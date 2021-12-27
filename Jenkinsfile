pipeline {
  agent any
 
  
 stages {
    stage ('Build with PyTest') {
      steps {
      
        sh ''' 
        py.test test_calc.py -v
        py.test test_person.py -v   

        echo SUCCESS
        echo Build Number is: ${BUILD_ID}
        '''
        
        //sh 'mvn clean install -f MyWebApp/pom.xml'
      }
    }
    stage ('Build with UnitTest') {
      steps {
        sh '''
        python test_person.py -v
        python test_calc.py -v

        echo SUCCESS
        echo Build Number is: ${BUILD_ID}
        '''
        //sh 'mvn clean install -f MyWebApp/pom.xml'
      }
    }
  
    stage ('Code Quality') {
      steps {
          echo "Reviewing Code"
        /* withSonarQubeEnv('SonarQube') {
        sh 'mvn -f MyWebApp/pom.xml sonar:sonar' */
        }
      }
    
    stage ('JaCoCo') {
      steps {
          echo "JaCoCo'ing now"
      //jacoco()
      }
    }
    stage ('Upload Artifact') {
      steps {
        sh '''
        echo "Uploading Artifact"
        sudo echo "Artifact # ${BUILD_ID} succesfully saved " > ~/index.html 
        '''
        
        /* nexusArtifactUploader(
        nexusVersion: 'nexus3',
        protocol: 'http',
        nexusUrl: 'nexus_url:8081',
        groupId: 'myGroupId',
        version: '1.0-SNAPSHOT',
        repository: 'maven-snapshots',
        credentialsId: 'fc0f1694-3036-41fe-b3e3-4c5d96fcfd26',
        artifacts: [
        [artifactId: 'MyWebApp',
        classifier: '',
        file: 'MyWebApp/target/MyWebApp.war',
        type: 'war']
        ]) */
      }
    }
    stage ('DEV Deploy') {
      steps {
      echo "deploying to DEV Env "
      // deploy adapters: [tomcat9(credentialsId: '268c42f6-f2f5-488f-b2aa-f2374d229b2e', path: '', url: 'http://your_public_dns:8080')], contextPath: null, war: '**/*.war'
      }
    }
    stage ('Slack Notification') {
      steps {
        echo "deployed to DEV Env successfully"
        //slackSend(channel:'your slack channel_name', message: "Job is successful, here is the info - Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
      }
    }
    stage ('DEV Approve') {
      steps {
      echo "Taking approval from DEV Manager for QA Deployment"
        timeout(time: 7, unit: 'DAYS') {
        input message: 'Do you want to deploy?', submitter: 'admin'
        }
      }
    }
     
  }
}
