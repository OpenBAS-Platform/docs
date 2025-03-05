# OpenBAS Agent

## Introduction

The OpenBAS Agent is an application whose main role is to enroll an Asset on the OpenBAS platform,
to retrieve jobs or scripts to be executed and to transmit this information to Implants (subject to come)
for execution on the host Asset.

The Agent will not perform direct actions on the Asset to remain neutral for antivirus and ensure the full run of the simulation.

The OpenBAS Agent is compatible with different OS (Windows, Linux, macOS) and is developed in Rust.

## Installation

Depending on the OS, several installations are at your disposal, you can find them on OpenBAS by clicking the blue icon on the right top corner :
![Agents](../administration/assets/agents.png)

Linux

- Requirement → systemd, access to the openbas instance used
- Compatibility → All systemd based linux distros

| Installation mode                         | Installation                                                                                                                                    | Installation type                                           | Execution agent and payload                                                           | Verification/Start/Stop agent                                                                                                                    | Folder (and Antivirus exclusion) path | Uninstallation                                                                                                                                                                                                    |
|:------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------------------------------------|:--------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------|:--------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Standard installation (session)           | Terminal with standard privilege                                                                                                                | User service: `systemctl --user`                            | Background, only when user is logged, with the user privilege and environment         | `systemctl --user enable openbas-agent-session` & `systemctl --user start openbas-agent-session` & `systemctl --user stop openbas-agent-session` | $HOME/.local/openbas-agent-session    | `systemctl --user stop openbas-agent-session & systemctl --user disable openbas-agent-session & systemctl --user daemon-reload & systemctl --user reset-failed & sudo rm -rf $HOME/.local/openbas-agent-session`  |
| Advanced installation as User (service)   | Terminal with sudo privilege (replace params USER and GROUP in the bash snippet and in the following commands by the username and group wanted) | Service: `systemctl` (with user and group in service conf)  | Background, as soon as the machine powers on, with the user privilege and environment | `systemctl enable USER-openbas-agent` & `systemctl start USER-openbas-agent` & `systemctl stop USER-openbas-agent`                               | /opt/openbas-agent-service-USER       | `sudo systemctl stop USER-openbas-agent & sudo systemctl disable USER-openbas-agent & sudo systemctl daemon-reload & sudo systemctl reset-failed & sudo rm -rf /opt/openbas-agent-service-USER`                   |                             
| Advanced installation as System (service) | Terminal with sudo privilege                                                                                                                    | Service: `systemctl`                                        | Background, as soon as the machine powers on, with the root privilege and environment | `systemctl enable openbas-agent` & `systemctl start openbas-agent` & `systemctl stop openbas-agent`                                              | /opt/openbas-agent                    | `sudo systemctl stop openbas-agent & sudo systemctl disable openbas-agent & sudo systemctl daemon-reload & sudo systemctl reset-failed & sudo rm -rf /opt/openbas-agent`                                          |

- If you want to allow your agent to launch commands payloads for a user without filling the sudo password, follow [this tutorial](https://gcore.com/learning/how-to-disable-password-for-sudo-command/)

MacOS

  - Requirement → launchd, access to the openbas instance used
  - Compatibility → All launchd based MacOS distros (10.4 Tiger or higher)
  - Installation → Create a service with name openbas-agent ("Install MacOS Agent")
  - Verification command line → `launchctl list | grep openbas.agent`
  - Start/Stop service → `launchctl bootstrap system ~/Library/LaunchDaemons/openbas-agent.plist` & `launchctl bootout system ~/Library/LaunchDaemons/openbas-agent.plist`

Windows

  - Requirement → Powershell "run as administrator", and ensure access to the OpenBAS instance being used. If the installation fails, try using PowerShell 7 or higher.
  - Compatibility → All major Windows versions
  - Installation → Create a service with name openbas-agent ("Install Windows Agent")
  - Verification command line → `Get-Service -Name "OBASAgentService"`
  - Start/Stop service → `Start-Service -Name "OBASAgentService"` & `Stop-Service -Name "OBASAgentService"`

The following flow diagram represents the Agent installation flow :

![img.png](../administration/assets/agent_installation_flow_diagram.png)

## Network Traffic

The installation creates two firewall rules.

Inbound rule
![Inbound rule](../administration/assets/inbound-rule.png)

Outbound rule
![Outbound rule](../administration/assets/outbound-rule.png)

## Features

The main features of the OpenBAS Agent are:

- Agent registration on the OpenBAS platform

  The Agent is installed on the Asset using an agent-installer.exe file and runs as a service.
  It communicates with the deployed OpenBAS instance in order to enroll the Asset. In some cases
  like unsecured certificates or environment with proxy, the agent can't communicate with OpenBAS.
  In order to fix those issues, look at "Network and security" chapter from [configuration](https://docs.openbas.io/latest/deployment/configuration)
  to add the required attributes.

  NB : An Asset can only have one OpenBAS agent installed thanks to a machine id calculated according
  to the operating system and its parameters. If you try to install again an OpenBAS agent on a platform, it will
  overwrite the actual one and you will always see one endpoint on the OpenBAS endpoint page.

![Agent assets status](../administration/assets/agent_assets_status.png)

- Auto upgrade the Agent (on start-up and registration)

- Retrieval of jobs to be executed

  The Agent retrieves jobs to be executed from the OpenBAS instance every 30 seconds.
  For the moment, jobs are Implant to spawn and launch on the Asset, waiting to execute payloads of your Simulation's Injects.
  Each job execution logs is kept in a dedicated directory in order to have a trace of what happened (pid, executable).

- Deleting executables and execution directories

  The Agent deletes Implants that have been running for a predefined time and cleans the execution directories.

- Health check

  The Agent pings the OpenBAS instance every 2 minutes to notify it of its healthy status.

- Cleanup

  The Agent ensures that the processes it has executed are correctly finished or deleted if necessary. 
  The maximum time in minutes that a process associated with an execution directory can remain active is 20 minutes.

  The Agent removes execution directories to avoid excessive disk space. 
  The maximum time in minutes that an execution directory can be kept before being deleted is 2 days.

## Troubleshooting

If you experience issues with your agent, the logs are available here (see the "Installation" section above to get the folder path) :

- Linux -> [FOLDER_PATH]/openbas-agent.log
- MacOS -> [FOLDER_PATH]/openbas-agent.log
- Windows -> [FOLDER_PATH]\openbas-agent.log

