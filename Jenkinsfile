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
            }

          }
        }

        stage('Create Backup folder') {
          steps {
            timestamps() {
              powershell 'mkdir Backup'
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
            }

          }
        }

        stage('Add Content') {
          steps {
            timestamps() {
              powershell 'Set-Content file.txt \'Succesful Pipeline!, Check your logs on Elastic\''
            }

          }
        }

        stage('Move textfile') {
          steps {
            timestamps() {
              powershell 'Move-Item file.txt Backup'
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
            }

          }
        }

        stage('Delete folder') {
          steps {
            timestamps() {
              powershell 'rm -r Backup'
            }

          }
        }

      }
    }

    stage('Move Zip') {
      steps {
        timestamps() {
          powershell 'Move-Item backup.gz Important'
        }

      }
    }

  }
}