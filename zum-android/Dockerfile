FROM brendanreis/crestron-mobile:android-base-1

RUN ${ANDROID_HOME}/tools/bin/sdkmanager --install "build-tools;28.0.3"

WORKDIR /agent
CMD ./config.sh --unattended --url https://dev.azure.com/crestron-mobile-devops/ --auth pat --token ${AGENT_TOKEN} --pool "Local Ubuntu" --agent "zum-android" --replace --acceptTeeEula && ./run.sh
