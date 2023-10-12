
### _**Lab 1**_

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
