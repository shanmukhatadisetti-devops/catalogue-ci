@Library('jenkins-shared-pipeline') _ 

def configMap = [
    project: "roboshop",
    component: "catalogue"
    ]

if( ! env.BRANCH_NAME.equalsIgnoreCase('main')) { 
   NodejsEKSPipelines(configMap)
} else{ 
   echo "Continue With CR Process" 
}