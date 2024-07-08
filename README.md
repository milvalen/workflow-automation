## Workflow Automation Review

This documentation provides an overview of the workflow automation code. The workflow involves adding a new lead, updating the expected closed date, and moving the lead through different stages.

### Adding a New Lead

- Add a lead with a specific email and expected closed date.
- Convert the lead to a deal to activate the workflow.
- The pipeline stage starts at "New Lead."

### Moving Through Stages

- Moving the lead to the first stage triggers a new activity task and a Slack notification with an appointment link.
- Moving to the follow-up stage generates a new notification with an invalid link.
- Transitioning to the last stage results in a message in the general channel about the lead being closed.

### Email Notifications

An email is sent automatically thanking the user for the subscription and requesting feedback.

### Workflow Mechanics

- The workflow is structured with stages like "New Lead" and "Follow-Up."
- Triggers include updating and adding deals or converting leads.
- Filters check for specific conditions before transitioning stages.

### Server-Side Configuration

The server-side configuration involves a dorker compose - a YAML file with ports and encryption settings.

## Installation

### 1. DNS setup

Add A Record to route the subdomain accordingly:

```
Type: A
Name: n8n (or the desired subdomain)
IP address: <IP_OF_YOUR_SERVER>
```

### 2. Create ```.env``` file

Create a .env file and change it accordingly.

```
# The top-level domain to serve from
DOMAIN_NAME=example.com

# The subdomain to serve from
SUBDOMAIN=n8n

# DOMAIN_NAME and SUBDOMAIN combined decide where n8n will be reachable from
# above example would result in: https://n8n.example.com

# Optional timezone to set which gets used by Cron-Node by default
# If not set New York Time will be used
GENERIC_TIMEZONE=Europe/Berlin

# The email address to use for the SSL certificate creation
SSL_EMAIL=user@example.com
```

### 3. Create data folder

Create the Docker volume that's defined as n8n_data. n8n will save the database file from SQLite and the encryption key in this volume.
```
sudo docker volume create n8n_data
```
Create a volume for the Traefik data, This is defined as ```traefik_data```.
```
sudo docker volume create traefik_data
```

### 4. Start Docker Compose

n8n can now be started via:
```
sudo docker compose up -d
```
To stop the container:
```
sudo docker compose stop
```

### 5. Import Workflow

n8n will now be reachable using the above-defined subdomain + domain combination.

n8n will only be reachable using ```https``` and not using ```http```.

Then create a new workflow page and import automation from the file ```My_workflow.json```
