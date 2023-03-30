pipeline {
  agent any
  
  stages {
    stage('Get user input') {
      steps {
        script {
          def clusterName = input(
            message: 'Enter the name of the ECS cluster:',
            parameters: [string(name: 'clusterName', defaultValue: '')]
          )
          def serviceName = input(
            message: 'Enter the name of the ECS service:',
            parameters: [string(name: 'serviceName', defaultValue: '')]
          )
          // Repeat for other parameters
          
          def stackName = "${clusterName}-${serviceName}-stack"
          def templateBody = readFile('ecs-service-template.json')
          def parameters = [            "ClusterName": clusterName,            "ServiceName": serviceName,            // Add other parameters          ]
          
          cfnCreateOrUpdate(stackName, templateBody, parameters)
        }
      }
    }
  }
  
  post {
    always {
      cfnCleanup()
    }
  }
}
