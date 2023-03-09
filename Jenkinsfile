pipeline { 
    agent any
    stages{
        stage('git checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/Subashini80/SRE.git'
            }
        }
        stage('UNIT testing'){
            steps{
                bat "C:\\ProgramFiles\\apache-maven-4.0.0-alpha-4\\bin\\mvn test"
            }
        }
        stage('Intregration Testing'){
            steps{
              bat "C:\\ProgramFiles\\apache-maven-4.0.0-alpha-4\\bin\\mvn verify -DskipUnitTests"  
            }
        }
        stage('maven build'){
            steps{
               bat "C:\\ProgramFiles\\apache-maven-4.0.0-alpha-4\\bin\\mvn clean install"  
            }
        }
        stage('Static code analysis'){
            steps{   
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-api') {
                         bat "C:\\ProgramFiles\\apache-maven-4.0.0-alpha-4\\bin\\mvn clean package"
                    } 
                }
            }
        }
        stage('upload file to Nexus'){
            steps{
                script{ 
                   pom = readMavenPom file: "pom.xml";
                    filesByGlob = findFiles(glob: "target/*.${pom.packaging}");
                    echo "${filesByGlob[0].name} ${filesByGlob[0].path} ${filesByGlob[0].directory} ${filesByGlob[0].length} ${filesByGlob[0].lastModified}"
                    artifactPath = filesByGlob[0].path;
                    artifactExists = fileExists artifactPath;
                    if(artifactExists) {
                        echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}";
                        nexusArtifactUploader(
                            nexusVersion: NEXUS_VERSION,
                            protocol: NEXUS_PROTOCOL,
                            nexusUrl: NEXUS_URL,
                            groupId: pom.groupId,
                            version: pom.version,
                            repository: NEXUS_REPOSITORY,
                            credentialsId: NEXUS_CREDENTIAL_ID,
                            artifacts: [
                                [artifactId: pom.artifactId,
                                classifier: '',
                                file: artifactPath,
                                type: pom.packaging],
                                [artifactId: pom.artifactId,
                                classifier: '',
                                file: "pom.xml",
                                type: "pom"]
                            ]
                        );
                    } else {
                        error "*** File: ${artifactPath}, could not be found";
                    }      
                }
            }
        }
    }
}      

