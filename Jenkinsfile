node {
    stage('Preparation') { // for display purposes
        // Get some code from a GitHub repository
        git 'https://github.com/vherawidatama/simple-python-pyinstaller-app.git'
    }
    withDockerContainer('python:2-alpine'){
        stage('Build') {
        echo 'Running Building Requirement....'
        sh 'python -m py_compile sources/add2vals.py sources/calc.py'
        }    
    }
    withDockerContainer('qnib/pytest') {
        // some block
        stage('Test') {
            sh 'py.test --junit-xml hasil/results.xml sources/test_calc.py'
            junit 'hasil/results.xml'
        }
    }
    stage('Manual Approval') {
	// some block
	input message: 'Lanjutkan ke tahap Deploy?'
    }
    stage('Deploy') {
        // some block
        sh 'docker run --rm -v /var/jenkins_home/workspace/submission-cicd-pipeline-vhput998/sources:/src cdrx/pyinstaller-linux:python2 \'pyinstaller -F add2vals.py\''
        archiveArtifacts artifacts: 'sources/add2vals.py', followSymlinks: false
        sh 'docker run --rm -v /var/jenkins_home/workspace/submission-cicd-pipeline-vhput998/sources:/src cdrx/pyinstaller-linux:python2 \'rm -rf build dist\''
        sleep time: 1, unit: 'MINUTES'	
    }
}
