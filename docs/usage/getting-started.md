# Getting started

!!! tip "Under construction"

    We are doing our best to complete this page. If you want to participate, don't hesitate to join the [Filigran Community on Slack](https://community.filigran.io) or submit your pull request on the [Github doc repository](https://github.com/OpenBAS-Platform/docs).

This guide aims to give you a full overview of the OpenBAS features and workflows. The platform can be used in various
contexts to handle Breach and Attack simulations at technical or strategical levels. OpenBAS has been designed as a part
of the Filigran XTM suite and can be integrated with [OpenCTI](https://filigran.io/solutions/open-cti/) to generate
meaningful attack scenarios based on real threat. OpenBAS is result-oriented with many dashboards helping you to
evaluate
you security posture given a defined context.

Here are some examples of use cases:

- Designing attack scenario based on real threat
- Evaluate your security posture against technical simulations on endpoints
- Enhance team skills by evaluating them during simulations along with your security systems
- Organize Capture The Flag with multiple challenges
- Conduct atomic testing

## Onboarding

The onboarding feature helps new users discover OpenBAS step by step, by guiding
them through essential configurations and workflows.

### Welcome popup

When you log in to OpenBAS for the first time, a **welcome popup** is displayed.  
This popup introduces you to the platform and lists all available tutorial videos.  
It is designed to give you a quick overview of the main concepts and help you
take your first steps with confidence.

![welcome-popup](assets/onboarding/welcome-popup.png)

### Contextual videos

On specific pages, you can trigger a contextual video tutorial that explains the
concepts and actions to perform:

- Discover OpenBAS
- Set up an endpoint
- Set up a collector
- Set up a player
- Set up a team
- Launch a scenario and understand your results

![contextual-video](assets/onboarding/contextual-video.png)

You can enable or disable these tutorials in your **platform settings** or in
your **user profile settings**.

### Getting started checklist

The onboarding wizard provides a **progress bar** showing the key actions you
need to complete before running your first scenario.

- Each task links directly to the relevant page and triggers its tutorial video.
- Completed actions are automatically marked as **done** in the wizard.
- Actions can also be skipped if you prefer to configure them later.

This checklist ensures you have everything set up before launching your first
Breach and Attack Simulation.

![checklist](assets/onboarding/checklist.png)

## Welcome dashboard

The welcome page provides every OpenBAS platform visitor with a snapshot of the platform activity as well as an overview
of your global security posture. You can find more information in [this section](evaluate/overview.md).

## Your first Breach and Attack Simulation

### Creating or Importing players and assets to play with

First, you need to create or import Players and Assets that will participate in the simulation and be targeted by
technical or strategical events. To do so, you can either create [players](people.md)
and [teams](people.md) or deploy agent on [assets](assets.md).

### Building your Scenario

Once integrations is done, you are ready to create your first Scenario!

[Scenarios](scenario.md) act as template for your Breach and Attack simulations. After establishing such a template, you
will be able to schedule it as a one shot simulation, or as a recurring one.

You have two main options to create scenarios:

#### Option 1: Import from XTM Hub
- Navigate to the Scenarios menu and click on **"Import from Hub"** to access the library of pre-built scenarios
- Browse scenarios by industry, attack type, or threat actor
- Download and import ready-to-use scenarios that match your testing requirements
- Customize the imported scenario for your specific environment

#### Option 2: Create from scratch
- Go to the Scenarios menu and create a new one with the + button.
- Now go to the [Injects](injects.md) tab and add some to build the serie of events that will define the core of your
  Scenario. If you want to stay strategical, you can select inject like "Send individual mails". If you want to go
  technical, you can select injects linked to attack pattern (Caldera integration allows you to play hundreds of them).
- Then, define [who or what will be targeted](targets.md) by those injects, customize them, and define what is expected
  to happen. For example, you expect the targeted team to perform a specific action and the animation team will
  validated this expectation manually. Or, you expect the technical event to be prevented and it will be automatically
  checked through your integrations with your security systems.
- Do not forget to define when the inject is played in the scenario chronology.

Optionally, you can enhance your scenario by
adding [Documents](components/documents.md), [Media pressures](components/media_pressure.md), or even
CTF [Challenges](components/challenges.md) to your injects.

### Play the simulation

You can now schedule your [Simulation](simulation.md) by hitting the blue "Simulate now" button. Choose your moment and
hit start.

On time, a Simulation based on your Scenario template is generated. It is listed in your Scenario overview and in the
Simulations menu. From there, you can follow the course of the Simulation and interact with it, for example to validate
manual expectations.

During the course of the simulation, results are updated and can be consulted in the Simulation overview.

### Evaluate your security posture

Results in OpenBAS are based on expectations' results that are linked to injects played during Simulations. It is then
important to manually validate expectations that need it.

Results are broken down by "Prevention", "Detection" and "Human response" metrics.

- Prevention displays your ability to prevent the scenario's technical events to be completed
- Detection displays your ability to detect the scenario's technical events
- Human response displays how well players and teams react as expected facing the scenario's events
- Vulnerability displays your ability to detect common vulnerabilities and exposures (CVEs) when the scenario's events happen.

!!! tip "Additional Resources"

    You can access additional Filigran resources and services through XTM Hub by clicking the 9-dot grid icon in the top navigation bar. This provides access to training materials, community resources, and other Filigran ecosystem services.
