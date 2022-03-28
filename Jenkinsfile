def records

pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/GauravGirase/FACTMigra.git'
            }
        }
        stage('ReadCSV') {
            steps {
                script{
                    records = readCSV file: 'JenkinsJobs.csv'
                }
            }
        }
        
        stage("Creating a job using csv"){
            
            steps{
                
            script{
              records.eachWithIndex{record, index ->
                    stage("Print parameters"){
                        echo "${index} :: ${record}" 
                    }
                    
                    stage("Build Job With Params"){
                        
                        echo "${record[2]}"
                        echo "${record[1]}"
                        
                        build job:'jobWithParams', parameters:[
                            string(name:"name", value:"${record[2]}"),
                            string(name:"Education", value:"${record[1]}")
                            ]
                        }
                    }  
                }
            }
        }
    }
}
