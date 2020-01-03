pipeline {
  agent any
  stages {
    stage('Folder Management') {
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
              logstash() {
                powershell 'mkdir Important'
              }

            }

          }
        }

        stage('Create Backup folder') {
          steps {
            timestamps() {
              logstash() {
                powershell 'mkdir Backup'
              }

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
              logstash() {
                echo 'Textfile creation'
              }

            }

          }
        }

        stage('Add Content') {
          steps {
            timestamps() {
              logstash() {
                powershell 'Set-Content file.txt \'Succesful Pipeline!, Check your logs on Elastic\''
              }

            }

          }
        }

        stage('Move textfile') {
          steps {
            timestamps() {
              logstash() {
                powershell 'Move-Item file.txt Backup'
              }

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
              logstash() {
                powershell 'tar -zcvf backup.gz Backup'
              }

            }

          }
        }

        stage('Delete folder') {
          steps {
            timestamps() {
              logstash() {
                powershell 'rm -r Backup'
              }

            }

          }
        }

      }
    }

    stage('Move Zip') {
      steps {
        timestamps() {
          logstash() {
            powershell 'Move-Item backup.gz Important'
          }

        }

      }
    }

  }
}