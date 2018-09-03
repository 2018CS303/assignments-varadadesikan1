# Assignment - 2

## Blue Ocean

1. As administrator move to `Manage Jenkins -> Manage Plugins`.
2. Choose `Available` plugins 
3. Install `Blue Ocean (BlueOcean Aggregator)` plugin.
4. Install Blue Ocean along with the required dependencies.
5. Restart Jenkins using ```bash sudo service jenkins restart```
6. Upon restart, enable the `Blue Ocean` option from the GUI.

## Private repository as FreeStyle Project

1. Setup a new project - `New Item -> Freestyle project`.
2. Under `Source Code Management` select `Git`.
3. Provide the private repository's URL in `Repository URL`.
4. To permit Jenkins to access the Private Github repository, update the credentials under `Add -> Credentials -> Jenkins`.
5. Set this as the `Credentials`.
6. Update the branch (if required) - Default : `*/master`.
7. Now the private repository can be used with Jenkins like any other repository.

## Git SCM Poll

1. Map the [Jenkins URL](http://localhost:8080/) to a public IP address.
  
  - Map a Public IP to your [Jenkins URL](http://localhost:8080/) using `ngrok`.
  - Download and setup `ngrok` from [here](https://ngrok.com/download).
  - Run `./ngrock http 8080` (map your Jenkins port (8080) to a public IP. The public URL `http://<foo>.ngrok.io` should be used as the Webhook.

2. Setup
  
  - Go to `Settings -> Webhooks -> Add webhook` in the repository.
  - Update the `Payload URL` to the Public IP `http://<foo>.ngrok.io/github-webhook/`.
  - Set `Content type` as `application/json`.
  - Update `Which events would you like to trigger this webhook?` as per requirement.
  - Ensure that the `Active` option is selected.

## Post-build Actions

1. Select the project and go to `Configure -> Post-build Actions`
2. Click on `Add post-build action`
3. Choose `Archive the artifacts`.
4. Mention the files to archive ( `*` to archive all the files).
5. In the `Advanced...` tab, enable `Archive only if build is successful` and `Use default excludes`.

