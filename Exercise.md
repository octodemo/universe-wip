<details>
<summary>Lab 1 : Get clean code using GitHub Copilot</summary>

In this exercise we will use GitHub Copilot to give us give us code suggestions for a Delete record usecase. The functionality we have to implement is, ask Copilot to create a function which deletes an art piece from the `gallery` table based on the `title` name and `gallery id`

1. Open the file `main.go` in the Codespace ide under the `gallery` folder in root
2. At the end of the `Update` function you can enter the below prompt to ask GitHub Copilot for the Go code to delte items from gallery table
3. If you see the code recommendation from GitHub Copilot, it has recommended an SQL operation using parameterized queries instead of user input appended queries
4. This demonstrates how GitHub Copilot filters out security vulnerabilities in code recommended. [Further reading](https://github.blog/2023-02-14-github-copilot-now-has-a-better-ai-model-and-new-capabilities/#filtering-out-security-vulnerabilities-with-a-new-ai-system)


`//write a function that deletes an art piece from the gallery table based on the title name and gallery id`

```
/ write a function that deletes a record from the gallery table based on the gallery id and title name
func (g Gallery) DeleteGallery(title string) error {
	db := GetDb()
	stmt, err := db.Prepare("DELETE FROM gallery WHERE title = ? and id = ?")
	if err != nil {
		return err
	}
	defer stmt.Close()
}

```
</details>

<details>
    <summary>Lab 2 : Use GitHub Copilot to generate regular expressions for custom secret patterns</summary>

#### Enabling secret scanning
Secret scanning can be enabled in the settings of an organization or a repository. If Advanced Security is not enabled yet, then enable that first (same settings screen).

1. Go to the repository settings and enable secret scanning in the `Code security and analysis` section.

#### Viewing and managing results
After a few minutes, the `Security` tab in the repository will indicate that there are new security alerts.

- Go to the `Secret scanning` section to view the detected secrets.

For each secret, look at the options to close it and determine which one is most suitable.

2. This source code already has a secret hardcoded in a properties file by the name `connection.properties` file under the `storage-service` root folder

The secret key `mona_value_abc124` is hardcoded in the properties file. We will use GitHub Copilot chat to get a suggestion of a regular expression that can be fed into the GitHub Custom Patterns for Secret Scanning. This exercise will demonstrate how GitHub Copilot can assist users and security architects and administrators to create high fidelity regular expressions when enough context about a secret pattern is given to GitHub Copilot

In the GitHUb Copilot for Chat window in the VS Code IDE, we can type in a prompt like below. Copilot will respond back with a regular expression pattern
`help me create a regular expression for the following string mona_value_`
Copilot will respond back with a regular expression pattern as shown below in the screen grab

![image](https://github.com/advanced-security-demo/mona-gallery/assets/79184790/aa7e0f84-4589-4daa-9972-db0c6d80de7b)

3. But here, let us give a little more context to GitHub Copilot, and ask it a very specific regular expression for the parrern under discussion. Assume that we know that the custom secret pattern always ends with an alphanumeric character of length 6. Lets rephrase our prompt in GitHub Copilot Chat and ask for a modified version of the regular expression. 

![image](https://github.com/advanced-security-demo/mona-gallery/assets/79184790/836d0a75-6838-412c-956a-46c2034176dd)

4. In this case if you see, GitHub copilot has given us a very specific regular expression which which checks for a the string `mona_value_abc124` and gave us a regex as follows `mona_value_[a-zA-Z0-9]{6}`

5. Next, navigate to your `Settings` section in your repository
6. Click on the `Code security and analysis` section on the left navigation pane
7. Next enable `Secret Scanning` option in the GitHub settings page
8. Under Seceet Scanning we will have a section called `Custom Patterns`. This is where we will create a new pattern to capture the secret `mona_value_abc124`. 
9. Click on `New Pattern` and key in a Pattern name & the regular expression prompted by GitHub Copilot in step 3 under the section `Secret format (specified as a regular expression)`
10. Provide a `Test string` to test that the regular expression captures your intended secret pattern. And then click on `Save and dry run`
11. Once the dry run in over, click on `Publish pattern`. With this step completed, you can navigate to `Security` section in the repository and you can see that a new secret has been identified by GitHub Secret Scanning and has been flagged as a vulnerability

![image](https://github.com/Ent-Org/mona-gallery/assets/79184790/c4ba9148-facb-44ad-92f5-8f9a854a56e9)

</details>

<details>
    
<summary>Lab 3: Use GitHub Copilot and AI to fix vulnerabilities in your code</summary>

#### Sanitize Input 

In this exercise we will attempt to remediate the SQL Injection vulnerability that exists in `main.go` on line 308. 

![image](https://github.com/octodemo/universe-wip/assets/68650974/c88eccf2-224d-4de9-a31c-3d555db65f67)

Input sanitization is a fundamental security practice to prevent SQL injection attacks.

1. Create a branch called `sql-injection-fix`. If using codespaces you can run the command `git checkout -b sql-injection-fix`

2. Add the following sanitization function on line 201 of `frontend/components/Gallery.vue`

```js
function sanitizeInput(input) {
    if (input == null) {
        return "";
    }
    // Replace all occurrences of apostrophe with two consecutive apostrophes
    input = input.replace("'", "''");
    // Remove all multi-line or single-line comments
    input = input.replace(/\/\*[\s\S]*?\*\/|\/\/.*/, "");
    //Remove all SQL comments
    input = input.replace("--", " ")
    // Remove all inline semicolons
    input = input.replace(";", "");
    return input;
}
```
Add the following to line 250 of `/frontend/components/Gallery.vue`
```
    artItem.description = sanitizeInput(artItem.description)
    artItem.title = sanitizeInput(artItem.title)
```

3. Commit and push the code to the `sanitize-input` branch. If running codespaces, you can runn the following git commands:
```bash
git add .
git commit -m "Added sanitization method to Gallery.vue"
git push --set-upstream origin sanitiza-input
```

4. Raise a Pull Request to the `main` branch and wait for CodeQL to complete analysis on the pull request


#### Autofix Feature

You should see the following on your pull request. 

![image](https://github.com/octodemo/universe-wip/assets/68650974/906ed843-8b36-4397-b972-f5cef437a4c6)

Our function only replaced the first occurance of the string. Autofix has suggested a fix to replace the string with a regular expression and uses the `g` flag to ensure all occurrences are replaced.

Commit the fix suggested by the autofix feature. 

#### Copilot

Our sanitize function only applies to the UI. We will still be vulnerable if we expose the Update method as an API or other medium. 
Let's ask Copilot how we could fix this sanization problem.

In codespaces use the sarif viewer to navigate to the SQL Injection vulnerability located in gallery/main.go on line 308.
Note if the Sarif Viewer is not loading the correct SARIF you can use the one provided in the universe-utils/go.sarif

1. Select the `Fix using Copilot Option'
![image](https://github.com/octodemo/universe-wip/assets/68650974/f0986539-e074-4403-b356-2fe49bd07ac4)

Copilot should propose the following fix. Click Accept

![image](https://github.com/octodemo/universe-wip/assets/68650974/ad41524c-409d-44f0-9950-bc4e5446e2fa)


2. Commit and push in your code. Wait until CodeQL has completed analysis and merge to Main

### XSS Vulnerability 

</details>




