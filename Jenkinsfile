pipeline{

  agent {
    label 'server1'
  }

  tools{
    maven 'mymaven'
  }

environment {
  Name = "Yahya"
}

  parameters{
    string defaultValue: 'Yahya', name:'Name'
    choice choices: ['dev', 'prod'], name: 'Location'
  }

  stages{
    stage('Build Stage'){
      steps{
            sh 'mvn clean package'
            sh 'echo This is build by $Name'
      }
  
    }

  stage('Test'){

    parallel{


      stage('Test A'){
        steps{
          sh 'echo "This is Test A"'
        }
      }
      stage('Test B'){
        steps{
          sh 'echo "This is Test B"'
        }
      }
    }
    post{
      success{
    sh 'echo The test has been successfull.'
        
      }
    }
  }

  stage('Archieve Stage'){
    steps{
     archiveArtifacts artifacts: '**/target/*.war'
    }
    
  }
    
  }

  
}




/*
pipeline
{

agent {
  label 'devServer'
}

parameters {
    choice choices: ['dev', 'prod'], name: 'select_environment'
}

environment{
    NAME = "John Doe"
}
tools {
  maven 'mymaven'
}

stages{

    stage('build')
    {
        steps {
            script{
                file = load "script.groovy"
                file.hello()
            }
            sh 'mvn clean package -DskipTests=true'
           
        }

        

    }

    stage('test')
    { 
        parallel {
            stage('testA')
            {
                agent { label 'devServer' }
                steps{
                    echo " This is test A"
                    sh "mvn test"
                }
                
            }
            stage('testB')
            {
                agent { label 'devServer' }
                steps{
                echo "this is test B"
                sh "mvn test"
                }
            }
        }
        post {
        success {
             dir("webapp/target/")
            {
            stash name: "maven-build", includes: "*.war"
                 }
                 }
            }

    }

    stage('deploy_dev')
    {
        when { expression {params.select_environment == 'dev'}
        beforeAgent true}
      
        agent { label 'devServer' }
        steps
        {
            dir("/var/www/html")
            {
                unstash "maven-build"
            }
            sh """
            cd /var/www/html/
            jar -xvf webapp.war
            """
        }
    }

    stage('deploy_prod')
    {
      when { expression {params.select_environment == 'prod'}
        beforeAgent true}
        agent { label 'prodServer' }
        steps
        {
             timeout(time:5, unit:'DAYS'){
                input message: 'Deployment approved?'
             }
            dir("/var/www/html")
            {
                unstash "maven-build"
            }
            sh """
            cd /var/www/html/
            jar -xvf webapp.war
            """
        }  
    }

   

    
}

}
*/
