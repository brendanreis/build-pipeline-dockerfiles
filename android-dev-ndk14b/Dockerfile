FROM brendanreis/crestron-mobile:android-base

ENV NDK_VERSION android-ndk-r14b
ENV NDK_ZIP ${NDK_VERSION}-linux-x86_64.zip
ENV PATH=${PATH}:${ANDROID_SDK}/platform-tools
ENV PATH=${PATH}:${ANDROID_SDK}/tools

RUN wget -q https://dl.google.com/android/repository/${NDK_ZIP} && \
    unzip -q ${NDK_ZIP} && \
    rm ${NDK_ZIP}
ENV ANDROID_NDK_HOME ${ANDROID_SDK}/${NDK_VERSION}

RUN yes | \
    ${ANDROID_SDK}/tools/bin/sdkmanager "platform-tools" "platforms;android-26" "build-tools;26.0.2" "cmake;3.6.4111459" && \
    ${ANDROID_SDK}/tools/bin/sdkmanager --uninstall "cmake;3.10.2.4988404"

WORKDIR /agent
CMD ./config.sh --unattended --url https://dev.azure.com/crestron-mobile-devops/ --auth pat --token ${AGENT_TOKEN} --pool "Local Ubuntu" --agent ${AGENT_NAME} --replace --acceptTeeEula && ./run.sh
