# Python-Record-Linkage

## Overview
This repository is dedicated to building a Python Record Linkage Machine Learning Model, aimed at providing a sophisticated solution to record linkage problems. It includes raw data from the project "Synthetic-Gold," transformation scripts, and training models.

## Repo Structure
The repository contains the following main folders and their contents:
- `./Data/Synthetic Gold`: Contains several parquet folders of different data from the project "Synthetic-Gold." For more information on this project, see the following [link to that repo](https://github.com/DOH-PJG1303/Synthetic-Gold)
- `./Scripts`: Contains two sub-folders:
  - `Compile Training Data`: Includes 4 scripts to transform the raw data into an ML training dataset.
  - `Train Model`: Currently contains 1 file related to training the ML model, with more to be added in the future.

## Setup
This section will guide you through setting up the required environment.

### Downloading Python
Install Python by downloading it from the [official website](https://www.python.org/downloads/).

### Downloading Visual Studio Code
Download and install Visual Studio Code (VS Code) from the [official website](https://code.visualstudio.com/download).

### Downloading and Configuring Git
1. Download Git from the [official website](https://git-scm.com/downloads).
2. Install Git and integrate it with VS Code by following [these instructions](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support).

### Cloning the Github Repository
1. Open VS Code terminal (CMD terminal).
2. Clone the repository by running:

```CMD
git clone https://github.com/DOH-PJG1303/Python-Record-Linkage.git
```

### Opening the Repository Folder in Github
Open the cloned repository folder in Github by navigating to the folder within VS Code.

### Creating a Virtual Environment
1. Open the VS Code terminal (CMD terminal).
2. Run the following command to create a virtual environment:
```CMD
python -m venv .venv
```

### Activating the Virtual Environment
Activate the virtual environment using the following command in the CMD terminal:
 ```CMD
 .venv\Scripts\activate
 ```

### Loading Libraries
Load all libraries from the "requirements.txt" file by running:
```CMD
pip install -r requirements.txt
```

## Github Basics
In Github, projects are often collaborative and involve several key actions that make it a powerful tool:

- <span style="color:red">Commit</span>: When you make changes to your project, you save them locally with a commit. It's like a snapshot of your work at that moment.
- <span style="color:green">Branch</span>: Creating branches allows you to work on different versions of the project simultaneously. It keeps your main project untouched while you experiment or develop a new feature.
- <span style="color:blue">Pull</span>: If others are working on the same project, you can update your local repository with the latest changes using pull.
- <span style="color:purple">Push</span>: After making changes and committing them locally, you can share those changes with others by pushing them to the remote repository.
- <span style="color:orange">Pull Request</span>: If you want your changes to be added to the main project, you can create a pull request. This allows others to review your code before it's merged.
- <span style="color:brown">Issues</span>: These are used to track tasks, enhancements, and other types of questions within a project.
- <span style="color:pink">Merge</span>: When a branch is ready, it can be merged into the main project, combining the changes.

## Contact
**Personal Email:** [pjgibson25@gmail.com](mailto:pjgibson25@gmail.com)
**Work Email:** [peter.gibson@doh.wa.gov](mailto:peter.gibson@doh.wa.gov)
**Name:** PJ Gibson

Feel free to contact me for any questions, concerns, or collaboration opportunities.
