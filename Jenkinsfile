pipeline {
  agent any
  stages {
    stage('Folder Managemen') {
      parallel {
        stage('Folders Creation') {
          steps {
            timestamps() {
              echo 'Folder Creation'
            }

          }
        }

        stage('Create Important folder') {
          steps {
            timestamps() {
              powershell 'mkdir Important'
              logstashSend(maxLines: 1000, failBuild: true)
            }

          }
        }

        stage('Create Backup folder') {
          steps {
            timestamps() {
              powershell 'mkdir Backup'
              logstashSend(maxLines: 1000, failBuild: true)
            }

          }
        }

      }
    }

    stage('Textfile Creation') {
      parallel {
        stage('Textfile Creation') {
          steps {
            timestamps() {
              echo 'Textfile creation'
              logstashSend(maxLines: 1000, failBuild: true)
            }

          }
        }

        stage('Add Content') {
          steps {
            timestamps() {
              powershell 'Set-Content file.txt \'Succesful Pipeline!, Check your logs on Elastic\''
              logstashSend(maxLines: 1000, failBuild: true)
            }

          }
        }

        stage('Move textfile') {
          steps {
            timestamps() {
              powershell 'Move-Item file.txt Backup'
              logstashSend(maxLines: 1000, failBuild: true)
            }

          }
        }

      }
    }

    stage('Zip & Delete') {
      parallel {
        stage('Zip folder') {
          steps {
            timestamps() {
              powershell 'tar -zcvf backup.gz Backup'
              logstashSend(maxLines: 1000, failBuild: true)
            }

          }
        }

        stage('Delete folder') {
          steps {
            timestamps() {
              powershell 'rm -r Backup'
              logstashSend(maxLines: 1000, failBuild: true)
            }

          }
        }

      }
    }

    stage('Move Zip') {
      steps {
        timestamps() {
          powershell 'Move-Item backup.gz Important'
          logstashSend(maxLines: 1000, failBuild: true)
        }

      }
    }

  }
}