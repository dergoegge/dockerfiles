FROM google/cloud-sdk:alpine

RUN apk --update add \
	nodejs-npm \
	openjdk8-jre

RUN gcloud  --quiet beta emulators firestore start --host-port nope:6666