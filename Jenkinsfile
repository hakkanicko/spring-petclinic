pipeline {
    agent any
    stages {
        stage('build and tests') {
            steps {
                withMaven(maven: 'M3') {
                    sh 'mvn clean install'
                    stash(name: 'binaries', includes: 'target/\\*.jar', useDefaultExcludes: true)
                }

            }
        }
        stage('static-analysis') {
            steps {
                node(label: 'build') {
                    sleep 5
                }

            }
        }
        stage('acceptance-test') {
            steps {
                parallel(
                        "edge": {
                            node(label: 'build') {
                                sleep 5
                            }


                        },
                        "chrome": {
                            node(label: 'build') {
                                sleep 5
                            }


                        },
                        "firefox": {
                            node(label: 'build') {
                                sleep 5
                            }


                        }
                )
            }
        }
        stage('staging') {
            steps {
                node(label: 'build') {
                    sleep 5
                    unstash 'binaries'
                }

            }
        }
        stage('manual-approval') {
            steps {
                echo 'Déploiement en Prod ? Oui bien sur vas y'
            }
        }
        stage('deploy') {
            steps {
                node(label: 'build') {
                    sleep 5
                    echo 'Fini !!!'
                    unstash 'binaries'
                }

            }
        }
    }
}
