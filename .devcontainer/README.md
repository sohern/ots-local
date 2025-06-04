# EDS devcontainer
This devcontainer is for use with VSCode. It can be added to the root of an EDS project created using the AEM X-Walk template (https://github.com/adobe-rnd/aem-boilerplate-xwalk) with the AEM Code Sync GitHub app added in the Github web client.

## Setting Up the EDS devcontainer
Perform the following steps to add the devcontainer to your EDS project:

1. Copy the .devcontainer folder to the root of your EDS project.

2. Download the AEM SDK from Adobe's [software distribution site](https://experience.adobe.com/#/downloads) and place it in .devcontainer.

3. Download the Universal Editor Service from Adobe's [software distribution site](https://experience.adobe.com/#/downloads) and place it in .devcontainer.

4. Copy the Z-scaler root and intermediate certificates and place them in the .devcontainer folder. The certificates should use the names zscaler-root.pem and zscaler-intermediate. pem respectively.

5. Install the Dev Containers extension in VSCode.

6. Open the project folder. VSCode will detect .devcontainer/devcontainer.json. And prompt you to reopen the project in a devcontainer.

Note: Do not check in the AEM SDK, Universal Editor Service, or Z-scaler certificates to Git.

## Using the EDS devcontainer
Perform the following to use the devcontainer:

1. Open a bash or zsh terminal window. Run `start-aem author`

2. Start a second terminal window and run `start-ues`

3. Access https://localhost:44302 and sign in to the AEM admin console.

4. Install the X-Walk template in AEM.

5. Access https://experience.adobe.com/#/aem/editor. Once the page loads, enter the page you want to edit in the Site URL field (for example: localhost:44302/content/ots-local/index.html)

