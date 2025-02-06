# Goal
The goal is to use a compose.yaml file that runs locally, to deploy the same services into azure container apps.

# Problem
Running ``docker compose up`` locally spins the containers up and sets them by default into the same network, so they can communicate with each other.
In azure container apps thats not the case, therefore the ``pma`` container can't communicate with the ``db`` container out of the box.

# Solution
Running
- ``az containerapp compose create -g learn-aks-rg --environment mycontainerenv123 --compose-file-path compose.yaml``
and then configuring ingress for the ``db`` container
- ``az containerapp ingress enable --name db --resource-group learn-aks-rg --type internal --target-port 3306 --transport tcp``