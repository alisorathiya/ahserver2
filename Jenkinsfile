//getGitChanges -> Groovy Script that will return if the code has changed or not. 
// CODE_CHANGES = getGitChanges()

pipeline {
    agent any
    
    // For defining custom environmental variables 
//  emviornment {} || Available through all the stages
    environment {
        NEW_VERSION = '1.3.0'
        DEVOPS_BATCH = 'MIFTAH DEVOPS BATCH - 01'
//         SERVER_CREDENTIALS =  credentials('alihusain-test-server-credentials')
    }
    
    
    
    
    options {
        // Timeout counter starts AFTER agent is allocated
        timeout(time: 59, unit: 'SECONDS')
    }
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
                echo "Building Java Version ${NEW_VERSION}"
            }
        }
         stage('test') {
             
             // Defining conditionals for each stage - when is used 
             //eg you only want to run the test on development branch build 
             // when refers to "When should this be executed"
             
//              when {
//                  expression  {
//                      //BRANCH_NAME : Environmental Variable for Jenkins that gives us all the branch name in the mentioned git repo
//              BRANCH_NAME == 'dev' || BRANCH_NAME =='master'
//                  }
//              }

             steps {
             echo "Testing Application for ${DEVOPS_BATCH}..."
            }
        }
         stage('deploy') {
            steps {
             echo "Deploying Application for ${DEVOPS_BATCH}..."   
                             // Required Plugins in order to use the below script : Credentials, Credentials Binding             
                withCredentials([
                    usernamePassword(credentials:'alihusain-test-server-credentials', usernameVariable: 'USER', passwordVariable: 'PWD')
                    ])  {
                    sh "userPASSWORD ${USER} ${PWD}"
                    // echo "userPASSWORD ${USER} ${PWD}"
                    // echo "userPASSWORD ${USERNAME} ${PASSWORD}"
        
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


// ENV Variables : 
//  http://localhost:8080/env-vars.html/
// For defining custom environmental variables 
//  emviornment {} || Available through all the stages




// Using CREDENTIALS in JENKINSFILE
// 1. Define Credentials in JENINS GUi
// 2. Extract Credentials using SERVER_CREDENTIALS  = credentials('your_credentials_id_here') || it will bind the credentials to the variable here
// 3. Requires Credentials Binding Plugin 
// 4. if you only need to use credentials for a particular stage you can define inside the stage as : 
// withCredentials([]){ usernamePassword(credentials : 'your_credentials_id_here', usernameVariable: USER, passwordVariable: PWD)}
// 5. The above line will fetch credentials and store in USER and PWD variable
