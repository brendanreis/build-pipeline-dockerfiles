FROM brendanreis/crestron-mobile:android-base

ENV NDK_VERSION android-ndk-r18b
ENV NDK_ZIP ${NDK_VERSION}-linux-x86_64.zip

RUN wget -q https://dl.google.com/android/repository/${NDK_ZIP} && \
    unzip -q ${NDK_ZIP} && \
    rm ${NDK_ZIP}
ENV ANDROID_NDK_HOME ${ANDROID_SDK}/${NDK_VERSION}

WORKDIR /agent
CMD ./config.sh --unattended --url https://dev.azure.com/crestron-mobile-devops/ --auth pat --token ${AGENT_TOKEN} --pool "Local Ubuntu" --agent ${AGENT_NAME} --replace --acceptTeeEula && ./run.sh
