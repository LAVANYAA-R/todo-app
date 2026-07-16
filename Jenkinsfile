// ═══════════════════════════════════════════════════════════════
// RVCE Todo App — Jenkins Declarative Pipeline
// Updated for Repository Root Structure
// ═══════════════════════════════════════════════════════════════

pipeline {
    agent any

    stages {

        //──────────────────────────────────────────────────────
        // Stage 1 : Checkout
        //──────────────────────────────────────────────────────
        stage('Checkout') {
            steps {
                echo '📥 Checking out source code...'
                checkout scm

                echo 'Repository Information'
                echo "Workspace: ${WORKSPACE}"
            }
        }

        //──────────────────────────────────────────────────────
        // Stage 2 : Verify Project Structure
        //──────────────────────────────────────────────────────
        stage('Verify Project Structure') {
            steps {
                script {

                    echo 'Checking repository structure...'

                    def requiredFiles = [
                        'package.json',
                        'Dockerfile',
                        'docker-compose.yml',
                        'README.md',
                        'Jenkinsfile'
                    ]

                    requiredFiles.each { file ->
                        if (!fileExists(file)) {
                            error "Missing required file: ${file}"
                        }
                    }

                    def requiredDirs = [
                        'client',
                        'server'
                    ]

                    requiredDirs.each { dir ->
                        if (!fileExists(dir)) {
                            error "Missing required directory: ${dir}"
                        }
                    }

                    echo "Project Structure Verified Successfully"
                }
            }
        }

        //──────────────────────────────────────────────────────
        // Stage 3 : Install Server Dependencies
        //──────────────────────────────────────────────────────
        stage('Install Server Dependencies') {
            steps {
                dir('server') {
                    script {
                        if (isUnix()) {
                            sh 'npm install'
                        } else {
                            bat 'npm install'
                        }
                    }
                }
            }
        }

        //──────────────────────────────────────────────────────
        // Stage 4 : Install Client Dependencies
        //──────────────────────────────────────────────────────
        stage('Install Client Dependencies') {
            steps {
                dir('client') {
                    script {
                        if (isUnix()) {
                            sh 'npm install'
                        } else {
                            bat 'npm install'
                        }
                    }
                }
            }
        }

        //──────────────────────────────────────────────────────
        // Stage 5 : Verify Environment
        //──────────────────────────────────────────────────────
        stage('Verify Environment') {
            steps {

                script {

                    if (isUnix()) {
                        sh 'node -v'
                        sh 'npm -v'
                        sh 'git --version'
                    } else {
                        bat 'node -v'
                        bat 'npm -v'
                        bat 'git --version'
                    }

                }

                echo 'Repository Verified Successfully'
                echo 'Frontend Found'
                echo 'Backend Found'
                echo 'Docker Configuration Found'
                echo 'Jenkinsfile Found'
                echo 'Project Ready for Deployment'
            }
        }

        //──────────────────────────────────────────────────────
        // Stage 6 : Build Complete
        //──────────────────────────────────────────────────────
        stage('Pipeline Complete') {
            steps {
                echo '''
==========================================
BUILD SUCCESSFUL
==========================================

GitHub Integration ✔
Repository Checkout ✔
Dependencies Installed ✔
Project Verified ✔

RVCE DevOps Laboratory Pipeline Completed

==========================================
'''
            }
        }
    }

    post {

        success {
            echo 'Pipeline executed successfully.'
        }

        failure {
            echo 'Pipeline execution failed.'
        }

        always {
            echo 'Build Finished.'
        }
    }
}