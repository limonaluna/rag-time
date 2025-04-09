# Getting started with this repository
For the project to run, you need to setup a few resources on Azure, and also prepare development environment for it. The following guide walks you through the steps.

## Azure Resource Setup
Pre-requisites for this repository are the following resources:

### Deploy Azure Resources
1. Deploy an Azure OpenAI service
2. Deploy an Azure OpenAI chat completion model (e.g. gpt-4o)
3. Deploy an Azure OpenAI embedding model (e.g. text-embedding-ada-002)
4. Deploy an Azure Storage Account (ADLS Gen2) with hierarchical namespace enabled
5. Deploy and Azure AI Search Service (if no networking requirements exist, you can choose "Free" or "Basic" tier, else "Standard" Tier S1)

#### Upload Sample Data
- Go to your Azure Storage Account and create a new container
- Upload the [Health Plan PDF documents](https://github.com/Azure-Samples/azure-search-sample-data/tree/main/health-plan)
![Uploaded documents](./../images/journey0-document-upload-healthplan.png)

- Get the **Connection String** from your Storage Account from the **Access Keys** page and save it to use later
![Connection String](./../images/journey0-storage-access.png)

#### Get embedding model connection information
![Embedding Model](./../images/journey0-embedding-model.png)

#### Create AI search index
For the purposes of this quickstart, all of the preceding resources must have public access enabled so that the Azure portal nodes can access them.
- Use the import function in AI Search to index the general network risks
- Make sure to use the "delimitedText" parsing method to capture the columns of the CSV
- Modify the index and make sure to adjust the retrievable, searchable fields etc --> refer to the screenshot for the index configuration
- Verify the success of the indexing process by querying the index in the portal through the search explorer
![AI Search Index configuration](media/ai_search_index_config.png)

#### Retrieve connection information
- Retrieve all required information regarding endpoints and keys from the Azure resources
- This will be needed to fill out the .env file



## Setup of Coding environment
There are several options how you can run this code. We are showcasing two approaches, one that is using Github Codespaces, and the other one to run locally on your machine using virtual environments

### Github Codespaces Setup
GitHub Codespaces is an instant, cloud-based development environment that uses a container to provide you with common languages, tools, and utilities for development.

When you create a GitHub Codespace, four processes occur:
1. A virtual machine and storage are assigned to your Codespace.
2. A container is created.
3. A connection to the Codespace is made.
4. A post-creation setup is made.

![Codespace Creation Process](./../images/journey0-codespace-creation-process.png)

Github Codespaces can be used via your organization (if your company has enabled it),or from your personal account. Usage through the personal account is free for up to 60 hours per month. More details [here](https://docs.github.com/en/billing/managing-billing-for-your-products/managing-billing-for-github-codespaces/about-billing-for-github-codespaces).


#### Prerequisites
To use GitHub Codespaces, you need:

- A personal GitHub account OR a Github Team/Enterprise account where Github Codespaces is enabled
- Access to GitHub Codespaces (included in GitHub Team, Enterprise, and some Individual plans)

#### Launching a Codespace
1. Navigate to this repository on GitHub.
2. Click the green **"Code"** button at the top right.
3. Select the **"Codespaces"** tab.
4. Click **"Create codespace on `main`"** (or another branch you want to work from).

GitHub will automatically provision a development container based on the detected environment (e.g., Node.js, Python, .NET) and open it in your browser using VS Code Web.

![Launch Codespace](./../images/journey0-launch-codespace.png)


#### Inside the Codespace
- Ready-to-code environment with language-specific tools pre-installed
- Access to a full-featured terminal and Git
- Built-in port forwarding for local servers or apps
- VS Code extensions automatically suggested based on the project


#### Saving Your Work
- Use Git inside the Codespace terminal or the **Source Control** tab to commit and push your changes back to the repo.
- Your changes are saved automatically when you commit.


### Local Setup
If you don't want to use Github Codespaces, you can use a Python Virtual Environment instead.
A Python virtual environment is an isolated space where you can install Python packages and dependencies specific to your project, without affecting your global Python setup or other projects.

It helps you:
- Avoid version conflicts between projects
- Keep your environment clean and reproducible
- Easily share dependencies via requirements.txt

#### Clone the repository
1. Copy the repository URL (from Github)
2. Open Visual Studio Code
3. Press `Ctrl+Shift+P` (or `Cmd+Shift+P` on macOS) to open the **Command Palette**
4. Type and select `Git: Clone`
5. Paste the repository URL (e.g. "https://github.com/limonaluna/rag-time.git")
6. Choose a local folder where the repo will be cloned
7. When prompted, click **"Open"** to open the repo in VS Code

![Clone repository locally](./../images/journey0-clone-repo-locally.png)

#### Create virtual environment
##### 1. If you're not already in the folder where you want the environment:
```bash
cd /path/to/your/project
```

##### 2. Create virtual environment
```bash
python -m venv .venv
```

##### 3. Activate virtual environment
On macOS/Linux/WSL:
```bash
source .venv/bin/activate
```

On Windows CMD:
```cmd
.venv\Scripts\activate.bat
```

On Windows PowerShell:
```powershell
.venv\Scripts\Activate.ps1
```

#### Install requirements
```bash
pip install -r requirements.txt
```

#### Select the interpreter in VS Code
- Press Ctrl+Shift+P (or Cmd+Shift+P on macOS) to open the Command Palette
- Search for and select Python: Select Interpreter
- Choose the interpreter that points to .venv


## Setup of environment
### Fill out .env variables
- Create .env file (in the root of the repository)
- Example for .env file is shown in the file "env.example"
- Fill out all environment variables with the required information