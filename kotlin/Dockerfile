#
# Licensed to the Apache Software Foundation (ASF) under one or more contributor
# license agreements.  See the NOTICE file distributed with this work for additional
# information regarding copyright ownership.  The ASF licenses this file to you
# under the Apache License, Version 2.0 (the # "License"); you may not use this
# file except in compliance with the License.  You may obtain a copy of the License
# at:
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software distributed
# under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR
# CONDITIONS OF ANY KIND, either express or implied.  See the License for the
# specific language governing permissions and limitations under the License.
#

FROM adoptopenjdk/openjdk8-openj9:x86_64-ubuntu-jdk8u162-b12_openj9-0.8.0

RUN rm -rf /var/lib/apt/lists/* && apt-get clean && apt-get update \
	&& apt-get install -y --no-install-recommends locales \
	&& rm -rf /var/lib/apt/lists/* \
	&& locale-gen en_US.UTF-8

ENV LANG="en_US.UTF-8" \
	LANGUAGE="en_US:en" \
	LC_ALL="en_US.UTF-8" \
	VERSION=8 \
	UPDATE=162 \
	BUILD=12

ADD proxy /kotlinAction

RUN rm -rf /kotlinAction/.classpath /kotlinAction/.gitignore /kotlinAction/.gradle /kotlinAction/.project /kotlinAction/.settings /kotlinAction/Dockerfile /kotlinAction/build

RUN cd /kotlinAction; ./gradlew oneJar

RUN rm -rf /kotlinAction/src

CMD ["java", "-jar", "/kotlinAction/build/libs/kotlinAction-all.jar"]
