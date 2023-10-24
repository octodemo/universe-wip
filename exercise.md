# Universe 2023 - Workshop Exercises

Welcome to the workshop **Harnessing AI: Next Level Strategies for Advanced Security**!
Below you will find a set of exercises to complete as a part of this workshop. There will be a set amount of time to complete each one.
We will provide a walkthrough of the solution after each exercise.
If you get stuck there are hints along the way. Additionaly you can access a GIF-based solution for each exercise and a video link is also available. 


## Lab 1 - Secret Scanning AI 

### Exercise 1 - AI-generated custom patterns

We are excited to be shipping the feature **AI-generated custom patterns** at Universe 2023.
In this exercise, we will generate a custom pattern using this feature. 
<details>
<summary>Prerequiste - secret scanning must be enabled for this exercise. This feature should already be enabled by default for for this repository. If not, please follow the instructions below to enable secret scanning. </summary>

1. Navigate to the `Settings` tab of the repository, click on the `Code security and analysis` section, and click `Enable` under secret scanning.

    ![secret-scanning-enablement](https://github.com/octodemo/universe-wip/assets/68650974/fd1e12ad-5f36-4a77-a3a5-6e97db61c6ad)

</details>

**Scenario**

You are a part of the security team, and it has been brought to your attention that the minio password `mona_value_abc124` for the object store has been leaked in the code!
You want to write a custom pattern to detect this.

1. Navigate to `Settings` tab of the repository, click on `Code security and analysis` section, and under `Custom Patterns` click on `New pattern`
2. In the top right hand corner, click on `Generate with AI`
     <details>
    <summary> Solution </summary>
       
    ![secret-scanning-custom-ai-setting](https://github.com/octodemo/universe-wip/assets/68650974/ae7156c6-268e-4b56-8cb5-ad30c5fd1a2f)
    
     </details>

3. Fill in the options `I want a regular expression that` and `Examples of what I am looking for`

    <details>
      <summary> Hint </summary>
      You want to find a string that starts with `mona_value_`
    </details>
    
    <details>
      <summary> Solution </summary>
      
      ![secret-scanning-mona-value](https://github.com/octodemo/universe-wip/assets/68650974/052be656-400a-4f25-a0be-9d9f90602f93)
   
    </details>
    
4. Assume that we know that the custom secret pattern always ends with an alphanumeric character of length 6. Can you make the regex pattern more precise? For the most accurate results, it is imperative when dealing with AI that we provide as much detail as possible with as much context as possible.

    <details>
      <summary> Hint </summary>
      Provide the AI with more details about the pattern. Consider factors such as length. What about character composition? Is it entirely numerical? 
    </details>

    <details>
      <summary> Solution </summary>
      
      ![mona-value-6](https://github.com/octodemo/universe-wip/assets/68650974/e7eca0d5-98fb-4425-9da8-e1ae8a282df1)

    </details>

### Exercise 2 - generic secret detection using AI

At Universe 2023 we will also be releasing the **generic secret detection using AI** feature. Enabling this feature will use an AI model to detect additional secrets beyond the secrets detected with regular expression.

1. Enable this feature by navigating to the `Settings` tab of the repository, click on the `Code security and analysis` section, and tick the checkbox `Use AI detection to find additional secrets` under secret scanning.

   <details>
      <summary> Solution </summary>
    
   ![generic-ai-secret](https://github.com/octodemo/universe-wip/assets/68650974/0519aa0d-75a8-45e3-9fc5-f8d34ffd9bb2)

    </details>

2. To view detected alerts, navigate to the `Security` tab, under `Secret Scanning`, click the `Other` option

   <details>
      <summary> Solution </summary>
    
     ![generic-ai-alert](https://github.com/octodemo/universe-wip/assets/68650974/d8649f81-df12-4207-b533-09aec4f4e523)

    </details>


 