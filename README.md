# DigitalOcean Weekend Cost Optimizer

This repository automates the process of "pausing" DigitalOcean Droplets over the weekend to save costs.

## How it works
1. **Friday 8:00 PM UTC**: The script takes a snapshot of any Droplet tagged `weekend-off` and then destroys the Droplet (stopping billing).
2. **Monday 7:00 AM UTC**: The script recreates the Droplet from the latest snapshot and deletes the temporary snapshot.

## Setup Instructions
1. **Tag your Droplets**: Add the tag `weekend-off` to any Droplet you want to include in this schedule.
2. **Create API Token**: Go to your DigitalOcean Control Panel -> API -> Tokens. Generate a "Read & Write" token.
3. **Add Secret to GitHub**:
   - In this GitHub Repo, go to **Settings** > **Secrets and variables** > **Actions**.
   - Click **New repository secret**.
   - Name: `DIGITALOCEAN_ACCESS_TOKEN`
   - Value: (Your DigitalOcean API Token)
4. **Configure Region/Size**: Edit the `monday-startup.yml` file to match your Droplet's Region and Size.

## Important Notes
- **IP Address**: Since Droplets are destroyed, the IP address will change. We recommend using a **DigitalOcean Reserved IP** and updating your DNS to point to that.
- **Data**: All data on the main disk is saved in the snapshot.
