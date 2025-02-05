# sonarscanner-for.net
Setting Up SonarQube, Sonar Scanner, and Analysing .NET Project
Prerequisites:
1. Java Development Kit (JDK):
•	Download and Install OpenJDK 17:
Download OpenJDK 17 (Temurin 17.0.14) from Adoptium.
•	Select Other Platforms and Versions.
•	Choose the Operating System based on your PC (e.g., Windows).
•	For Architecture, select x64.
•	Under Package Type, select JDK.
•	 Choose Version 17 (LTS).
•	No Environment Variables Needed:
No need to set environment variables for Java, as SonarQube will automatically detect it.
•	Verify the Installation:
To verify the Java installation, run the following command in Command Prompt:
java -version
You should see an output like:
openjdk version "17.0.14" 2025-01-21
OpenJDK Runtime Environment Temurin-17.0.14+7 (build 17.0.14+7)
OpenJDK 64-Bit Server VM Temurin-17.0.14+7 (build 17.0.14+7, mixed mode, sharing)
2. SonarQube:
2.1 Download SonarQube Community Edition:
•	Visit the SonarQube Downloads page.
•	Download the latest version of the SonarQube Community Edition ZIP file.
2.2 Extract SonarQube:
•	Create a folder under *C:* (e.g., C:\sonarqube).
•	Extract the contents of the downloaded SonarQube ZIP file into this folder.
•	Example path after extraction: C:\sonarqube\sonarqube-25.2.0.102705.
2.3 Navigate to the SonarQube Installation Directory:
•	Open PowerShell as Administrator.
•	Navigate to the bin\windows-x86-64 directory where SonarQube is installed:
PS C:\> cd C:\sonarqube\sonarqube-25.2.0.102705\bin\windows-x86-64
2.4 Start the SonarQube Service:
•	To start the SonarQube service, execute the following command in PowerShell:
PS C:\sonarqube\sonarqube-25.2.0.102705\bin\windows-x86-64> net start SonarQube
•	Upon successful execution, you should see:
The SonarQube service is starting.
The SonarQube service was started successfully.
2.5 Stop the SonarQube Service:
•	To stop the SonarQube service, execute the following command:
PS C:\sonarqube\sonarqube-25.2.0.102705\bin\windows-x86-64> net stop SonarQube
•	After running the command, you will see:
The SonarQube service is stopping.
The SonarQube service was stopped successfully.
2.6 Access SonarQube:
•	Once the service is started, you can access SonarQube by opening your web browser and going to:
http://localhost:9000
3. Sonar Scanner for .NET:
•	Install SonarScanner for .NET globally (no need to install it in each project).
•	To install SonarScanner, run the following command:
dotnet tool install --global dotnet-sonarscanner
•	This will ensure that SonarScanner is available for all projects.

Steps to Set Up and Analyze a .NET Project with SonarQube:
Step 1: Creating a Project in SonarQube
1.	Open SonarQube in Your Browser:
Go to http://localhost:9000.
2.	Log In:
Log in using your credentials (default: admin/admin).
3.	Create a Project:
On the SonarQube dashboard, click on Create Project.
4.	Enter Project Name:
Give your project a name (e.g., MyWebApp).
5.	Generate an Authentication Token:
o	Go to My Account (top-right corner), then Security.
o	Under Generate Tokens, give the token a name (e.g., sqa_token), and click Generate.
o	Copy the generated token (e.g., sqa_0b14e6348087dccc32b99893f3bb7cbb64239566) for later use.
6.	Select Application Type:
When prompted, select .NET as the application type.
o	Choose .NET Core (or .NET Framework, if applicable).
o	Follow the instructions with the commands provided to run the analysis.
Step 2: Set Up the .NET Project for Analysis
1.	Navigate to the Project Directory:
Go to the root directory of your .NET solution (the folder containing the .sln file).
2.	Open Command Prompt:
Open Command Prompt in this directory.
Step 3: Run Sonar Scanner Analysis on Your Project
1.	Begin the SonarQube Analysis:
o	Run the following command to start the analysis:
dotnet sonarscanner begin /k:"demo2" /d:sonar.host.url="http://localhost:9000" /d:sonar.token="sqa_0b14e6348087dccc32b99893f3bb7cbb64239566"
	/k:"demo2": Project key (use the one created in SonarQube).
	/d:sonar.host.url="http://localhost:9000": SonarQube URL.
	/d:sonar.token="sqa_0b14e6348087dccc32b99893f3bb7cbb64239566": Authentication token generated earlier.
2.	Build the Project:
o	After starting the analysis, run:
dotnet build
3.	End the SonarQube Analysis:
o	After the build is complete, end the analysis by running:
dotnet sonarscanner end /d:sonar.token="sqa_0b14e6348087dccc32b99893f3bb7cbb64239566"
Step 4: Check the Results in SonarQube
1.	Access SonarQube Dashboard:
Open your SonarQube dashboard at http://localhost:9000.
2.	Log In:
Log in to the SonarQube interface.
3.	View Your Project:
Go to Projects on the left sidebar, and click on your project (e.g., demo2 or the name you selected).
4.	Review Issues:
You'll be able to see:
•	Bugs
•	Vulnerabilities
•	Code Smells
•	Duplications
•	Coverage
•	Accepted issues.
•	Security
•	Reliability
•	Maintainability
 

Step 5: Review SonarQube Issues
•	Navigate through the dashboard to review various issues related to your project.
•	SonarQube will highlight any potential problems such as:
•	Coding issues (bugs, vulnerabilities, etc.).
•	Code smells (areas of the code that could be improved).
•	Duplicated code.
•	Test coverage and other important metrics.

