/*
 * Licensed to the Apache Software Foundation (ASF) under one
 * or more contributor license agreements.  See the NOTICE file
 * distributed with this work for additional information
 * regarding copyright ownership.  The ASF licenses this file
 * to you under the Apache License, Version 2.0 (the
 * "License"); you may not use this file except in compliance
 * with the License.  You may obtain a copy of the License at
 *
 *     http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing,
 * software distributed under the License is distributed on an
 * "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
 * KIND, either express or implied.  See the License for the
 * specific language governing permissions and limitations
 * under the License.
 */

try {
node('Windows') {
        def JAVA_JDK_8=tool name: 'JDK 1.8 (latest)', type: 'hudson.model.JDK'
        echo "Testing with Java $JAVA_JDK_8"
        stage('JAVA'){
        withEnv(["Path+JDK=$JAVA_JDK_8\\bin","JAVA_HOME=$JAVA_JDK_8"]) {
                bat "echo %JAVA_HOME%"
                }
        } //end stage JAVA
    } // end node Windows
} // end try

finally {
    node('ubuntu') {
        emailext body: "See ${env.BUILD_URL}", recipientProviders: [[$class: 'CulpritsRecipientProvider'], [$class: 'FailingTestSuspectsRecipientProvider'], [$class: 'FirstFailingBuildSuspectsRecipientProvider']], replyTo: 'users@infra.apache.org', subject: "${env.JOB_NAME} - build ${env.BUILD_DISPLAY_NAME} - ${currentBuild.result}", to: 'gmcdonald@apache.org'
    }
}
