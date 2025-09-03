# NJ Courts Download Per File Number

An automated UiPath RPA (Robotic Process Automation) solution for downloading court documents from the New Jersey Courts website based on docket numbers.

## Overview

This project automates the process of searching and downloading court documents from the New Jersey Courts web portal. It uses UiPath Studio to create a comprehensive automation workflow that can handle large volumes of docket number searches and document downloads.

## Features

- **Automated Court Document Downloads**: Searches and downloads documents from NJ Courts website using docket numbers
- **Batch Processing**: Handles multiple docket numbers in a single run
- **Error Handling**: Comprehensive error handling with email notifications
- **Resume Capability**: Can resume interrupted processes using resume logs
- **Anti-Captcha Integration**: Includes anti-captcha plugin for automated captcha solving
- **Database Integration**: Stores transaction data in SQL Server database
- **Email Notifications**: Sends status updates and error reports via email
- **County Mapping**: Maps zip codes to New Jersey counties for proper court jurisdiction

## Project Structure

```
├── Data/
│   ├── Config.xlsx                    # Main configuration file
│   ├── EmailTemplates/               # Email notification templates
│   ├── Externals/                    # External plugins (anti-captcha)
│   └── User/                         # User-specific configuration files
├── Documentation/
│   └── REFramework Documentation-EN.pdf
├── Framework/                        # Core framework workflows
├── MOLStandardFramework/            # Standard framework components
├── Project/                         # Main project workflows
│   └── NJCourtsWeb/                # NJ Courts specific workflows
├── Reusable_Components/             # Reusable automation components
├── Main.xaml                       # Main entry point
└── project.json                    # Project configuration
```

## Prerequisites

- **UiPath Studio** (Version 25.0.167.0 or compatible)
- **Windows Operating System**
- **Google Chrome** browser
- **SQL Server** (for database operations)
- **Microsoft Outlook** (for email notifications)
- **Anti-Captcha Plugin** (included in Externals folder)

## Installation

1. **Clone or download** this project to your local machine
2. **Open UiPath Studio** and load the project
3. **Install required packages** (automatically handled by UiPath):
   - UiPath.Excel.Activities (2.24.4)
   - UiPath.Mail.Activities (2.0.11)
   - UiPath.PDF.Activities (3.20.2)
   - UiPath.System.Activities (25.4.4)
   - UiPath.UIAutomation.Activities (25.10.4)

## Configuration

### 1. Database Configuration
Update the connection string in `Data/User/connstring.txt`:
```
Server=localhost\SQLEXPRESS;Database=master;Trusted_Connection=True;
```

### 2. Chrome Browser Setup
Configure Chrome profile in `Data/User/ScriptToOpenChrome.txt`:
```powershell
$chromePath = "C:\Program Files\Google\Chrome\Application\chrome.exe"
$profileName = "RobotMaster"
```

### 3. Main Configuration
Edit `Data/Config.xlsx` to configure:
- Queue names and folders
- Email settings
- Processing parameters
- File paths

### 4. Anti-Captcha Setup
1. Install the anti-captcha plugin from `Data/Externals/anticaptcha-plugin_v0.62.crx`
2. Run the registry file `Data/Externals/anticaptcha-plugin.reg`
3. Configure your anti-captcha API key

## Usage

### Running the Process

1. **Open UiPath Studio** and load the project
2. **Configure parameters** in the Main.xaml arguments:
   - `in_OrchestratorQueueName`: Queue name for processing
   - `in_OrchestratorQueueFolder`: Folder containing the queue
   - `countDocket`: Number of docket numbers to process
   - `startDocketNumber`: Starting docket number
   - `in_UsrWorkYear`: Work year for processing
   - `in_DocketType`: Type of docket to process
   - `shouldUseAutoLogin`: Enable/disable auto-login

3. **Run the process** from UiPath Studio or deploy to UiPath Orchestrator

### Input Data Format

The process expects docket numbers in the configured queue. Each transaction should contain:
- Docket number
- Case type
- Processing parameters

## Key Workflows

### Main Components

- **Main.xaml**: Entry point and main orchestration
- **Framework/Process.xaml**: Core processing logic
- **Project/SetupEnvironment.xaml**: Environment initialization
- **Project/OpenAndLoginToNJCourts.xaml**: NJ Courts website login
- **Project/NJCourtsWeb/**: NJ Courts specific operations

### NJ Courts Web Operations

- **SearchForLeadsByDocketNumber.xaml**: Search for cases by docket number
- **DownloadCaseActionsFromNjCourts.xaml**: Download case documents
- **NavigateToAttachedDocument.xaml**: Navigate to document pages
- **TryDownloadingUsingAskToSaveMethod.xaml**: Download documents

### Error Handling

- **ReportErrorsToSupport.xaml**: Error reporting system
- **TakeScreenshot.xaml**: Screenshot capture for debugging
- **Email notifications**: Automatic error notifications

## Document Types Supported

The system can download various court document types including:
- Complaints
- Foreclosure documents
- Amended complaints
- Final judgements
- Last stipulations
- Stipulation of dismissal
- Proof of mailing

## County Mapping

The system includes a comprehensive mapping of New Jersey zip codes to counties in `Data/User/ZipCodeToCountyName.txt`, supporting all 21 counties in New Jersey.

## Monitoring and Logging

- **Transaction Logs**: Detailed logging of all transactions
- **Success/Failure Logs**: Separate logs for successful and failed downloads
- **Resume Logs**: Enable process resumption after interruptions
- **Email Notifications**: Status updates and error reports

## Troubleshooting

### Common Issues

1. **Chrome Profile Issues**: Ensure Chrome profile is properly configured
2. **Database Connection**: Verify SQL Server connection string
3. **Anti-Captcha**: Check API key configuration
4. **Network Issues**: Verify internet connectivity and NJ Courts website access

### Error Handling

The system includes comprehensive error handling:
- Automatic retry mechanisms
- Screenshot capture on errors
- Email notifications for critical errors
- Resume capability for interrupted processes

## Security Considerations

- Database credentials are stored in configuration files
- Email credentials should be properly secured
- Anti-captcha API keys should be protected
- Regular security updates for UiPath and dependencies

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

For technical support or questions about this automation:
- Check the error logs in the project directory
- Review email notifications for error details
- Ensure all prerequisites are properly installed and configured

## Version Information

- **Project Version**: 5.0.0
- **UiPath Studio Version**: 25.0.167.0
- **Target Framework**: Windows
- **Expression Language**: VisualBasic

---

**Note**: This automation is designed specifically for the New Jersey Courts website and may require updates if the website structure changes. Regular maintenance and testing are recommended.
