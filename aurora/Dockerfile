FROM brendanreis/crestron-mobile:android-base-1

WORKDIR /agent
CMD ./config.sh --unattended --url https://dev.azure.com/crestron-mobile-devops/ --auth pat --token ${AGENT_TOKEN} --pool "Local Ubuntu" --agent "aurora" --replace --acceptTeeEula && ./run.sh
