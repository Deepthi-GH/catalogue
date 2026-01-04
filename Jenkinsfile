@Library('jenkins-shared-library')

def configMap = [
    project: "roboshop",
    component: "catalogue"
]

echo "going to execute jenkins shared library"
//if branch is not equal to main,then run CI pipeline
if( ! env.BRANCH_NAME.equalsIgnoreCase('main') ) {
    nodejsEKSPipeline(configMap)
}
else {
 echo "please follow the CR process"
}
