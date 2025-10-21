# GitHub Checks
 
GitHub checks allows you to enforce security controls by blocking Pull Requests that are failing specific controls (ie; compromised NPM packages or vulnerable workflows). For more information, see [here](https://docs.stepsecurity.io/github-checks). 

This Repository contains some basic workflows and files that will trigger StepSecurity GitHub Check failures. Feel free to add your own context for testing purposes as well. 

## GitHub Check Controls:
* **NPM Package Compromised Updates** - Blocks PR's attempting to merge known compromised NPM packages
* **NPM Package Cooldown** - Blocks PR's attempting to merge a recently release version (cooldown period is configurable)
* **PWN Request** - Blocks PR's containing insecure workflow configurations that allows exploitation through maliscious forked PR's  
* **Script Injection** - Blocks PR's containing workflows that use overly permissive triggers or unsanitized external inputs

### Policy Set Up and Triggering Detections
* Create a GitHub Checks Policy for this repository under the GitHub [Checks tab] 
* Ensure all 4 controls are enabled (you can choose Optional checks or Required), and ensure that Optional Checks **are enabled for the repository you are testing**
* This repository contains a branch [vuln-branch](), which can be used as reference for triggering the following detections upon opening a PR:
  
#### 1. NPM Package Compromised Updates
* Introduces a compromised NPM package into the package.json (ansi-regex 6.2.1). Feel free to add your own compromised NPM package for testing

#### 2. PWN Request
* Introduces a workflow using a risky trigger (pull_request_target) and does not checkout the code using an explicit ref

#### 3. Script Injection
* Introduces a workflow executing untrusted input from context variables (ie. github.event.pull_request.title)

#### (Test coming soon for NPM Cooldown Check - feel free to introduce a recently released package to test this)

### Once you have set up GitHub Checks Policy, any pull request opened will now undergo StepSecurity Checks, per the policy that has been set above. You can view results and context directly within the PR, or centrally within the StepSecurity Dashboard.
