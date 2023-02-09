//getGitChanges -> Groovy Script that will return if the code has changed or not. 
// CODE_CHANGES = getGitChanges()

pipeline {
    agent any
    
    environment {
  NEW_VERSION = "1.3.0"
  DEVOPS_BATCH = "MIFTAH DEVOPS BATCH - 01"
}

    // parameters{
    //     // string(name:'VERSION',defaultValue: '', description:'version to deploy')

    //     // choices of version that needs to be deployed
    //     choice(name:'VERSION',choices:['1.1.0','1.2.0','1.3.0'],description:'')

    //     //if you want to skip certain stage on some builds 
    //     booleanParam(name:'executeTests',defaultValue: true, description:'version to deploy')
    // }

        parameters {
  choice choices: ['1.1.0', '1.2.0', '1.3.0'], description: 'Select any version', name: 'VERSION'
  booleanParam defaultValue: true, description: 'version to deploy', name: 'executeTests'
                    }

tools {
    //currently 3 tools are available in jenkins : jdk maven gradle
    // maven 'Maven'
    jdk 'JAVA-9'
}



    // For defining custom environmental variables 
//  emviornment {} || Available through all the stages
  
    // options {
    //     // Timeout counter starts AFTER agent is allocated
    //     timeout(time: 59, unit: 'SECONDS')
    // }
    stages {
        stage('build') {
            
//               when {
//                  expression  {
//                      //BRANCH_NAME : Environmental Variable for Jenkins that gives us all the branch name in the mentioned git repo
//                      // In this case it will check if branch is dev and if the code has changed or not
//              BRANCH_NAME == 'dev' && CODE_CHANGES == true
//                  }
//              }
            
            
            steps {
                echo "Building Application for ${DEVOPS_BATCH}..."
                echo " Choice : %choice%"
                // echo "Building Java Version ${NEW_VERSION}"
                echo "Installing JAVA 9 ..."
                // bat "java --version"
                sh "java --version"
                // echo "Java Installed"
                // bat "echo 'using bat"
              
            }
        }
         stage('test') {
             
when{
    expression {

        // BRANCH_NAME== 'main'
        params.executeTests

    }
}


// end 


             // Defining conditionals for each stage - when is used 
             //eg you only want to run the test on development branch build 
             // when refers to "When should this be executed"
             
            //  when {
            //      expression  {
            //          //BRANCH_NAME : Environmental Variable for Jenkins that gives us all the branch name in the mentioned git repo
            //  BRANCH_NAME == 'dev' || BRANCH_NAME =='master'
            //      }
            //  }

             steps {
             echo "Testing Application for ${DEVOPS_BATCH}..."
            }
        }
         stage('deploy') {
            steps {
             echo "Deploying Application for ${DEVOPS_BATCH}..."   
                             // Required Plugins in order to use the below script : Credentials, Credentials Binding                              
                 
                 withCredentials([usernamePassword(credentialsId: 'alihusain-test-server-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {

                    // sh "userPASSWORD ${USER} ${PWD}"
                    // echo "userPASSWORD ${USER} ${PWD}"
                    echo "userPASSWORD ${USERNAME} ${PASSWORD}"
                    echo "deploying version ${params.VERSION}..."
        
                }
            }
        }
    }
    // Post refers to execution of certain tasks / scripts after all the stages have been executed
    post {
    
        always {
            echo "always... ${DEVOPS_BATCH}"
            echo "BATCH NAME : ${DEVOPS_BATCH}"
            echo "NEW VERSION : ${NEW_VERSION}"
        // will execute whether build has failed or not || eg : email to the team about the status of the jobs
        }
        
        success {
        // it will execute only when all the stages have been succesfully executed
        echo "success : all the stages for ${DEVOPS_BATCH} have been succesfully executed"
        }
        
        failure {
        // it will execute if any of the stages have failed
        echo "FAILURE : some of the stages for ${DEVOPS_BATCH} have failed"
        }
        
        //other conditions : Build Status  or Build Status Changes
        
    }
}



// Reference Video : https://www.youtube.com/watch?v=7KCS70sCoK0

// ENV Variables : 
//  http://localhost:8080/env-vars.html/
// For defining custom environmental variables 
//  emviornment {} || Available through all the stages




// Using CREDENTIALS in JENKINSFILE
// 1. Define Credentials in JENINS GUi
// 2. Extract Credentials using SERVER_CREDENTIALS  = credentials('your_credentials_id_here') || it will bind the credentials to the variable here
// 3. Requires Credentials Binding Plugin 
// 4. if you only need to use credentials for a particular stage you can define inside the stage as : 
// withCredentials([]){ usernamePassword(credentialsId : 'your_credentials_id_here', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')}
// 5. The above line will fetch credentials and store in USER and PWD variable



// PARAMETERS IN JENKINSFILE

// Types of Parameters : 
// 1.  string(name,defaultValue,description)
// 2. choice


//Validate your syntax in jenkins
// https://opensource.triology.de/jenkins/pipeline-syntax/


// GITPOD FOR JENKINS : 
// https://github.com/alisorathiya/gitpod-jenkins
// run : docker-compose up



// Installing JENKINS ON WINDOWS : 
// https://youtu.be/XuMrEDA8cAI
//webhook