pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
		    echo 'Hello'
		    echo "$(pwd)"
                // checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'demoGithub', url: 'https://github.com/rincool/demoKatalon']])
            }
        }
	    stage('Run Katalon Docker') {
	        steps {
	        dir('/var/lib/jenkins/workspace/2_JenkinsFromSCM'){
                sh 'docker run -t --rm -v "$(pwd)":/tmp/project katalonstudio/katalon katalonc.sh -projectPath=/tmp/project -retry=0 -testSuitePath="Test Suites/demoJenkins" -browserType="Chrome (headless)" -executionProfile="default" -apiKey="371f4efd-e5bf-4724-9248-11421c1476db" --config -proxy.auth.option=NO_PROXY -proxy.system.option=NO_PROXY -proxy.system.applyToDesiredCapabilities=true -webui.autoUpdateDrivers=true'
                }
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'Reports/**/*.*', fingerprint: true
            junit 'Reports/**/JUnit_Report.xml'
        }
    }
}
