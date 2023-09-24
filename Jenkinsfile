node {
    stage('SCM Checkout') {
        echo 'checkout stage started'
        checkout([
            $class: 'GitSCM',
            branches: [[name: '*/master']], // Change to your desired branch
            doGenerateSubmoduleConfigurations: false,
            extensions: [[$class: 'CloneOption', noTags: false, reference: '', shallow: false]],
            userRemoteConfigs: [[url: 'https://github.com/Aabhas28/DemoJenkinsfile']],
            // Credentials ID for Git access (if required)
             credentialsId: 'Aabhas28/Pubgmobile@28',
        ])
        echo 'checkout stage completed'
    }
    stage('Compile Stage') {        
        echo 'compile stage started'
        def mvnHome = tool name: 'maven-3-9-4', type: 'Maven'
        bat "${mvnHome}/bin/mvn clean compile"
        echo 'compile stage completed'
    }
    stage('Test Stage') {        
        echo 'test stage started'
        def mvnHome = tool name: 'maven-3-9-4', type: 'Maven'
        bat "${mvnHome}/bin/mvn test"
        echo 'test stage completed'
    }
    stage('SonarQube Stage') {        
        echo 'sonarqube stage started'
        def sonarscannerHome = tool name: 'sonarqube-scanner', type: 'SonarScanner'
        bat "${sonarscannerHome}/bin/sonar-scanner"
        echo 'sonarqube stage completed'
    }
    stage('Deploy Stage') {        
        echo 'deploy stage started'
        def mvnHome = tool name: 'maven-3-9-4', type: 'Maven'
        bat "${mvnHome}/bin/mvn install"
        echo 'deploy stage completed'
    }
}

