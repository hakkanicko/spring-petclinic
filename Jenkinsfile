pipeline {
    agent none
    stages {
        stage('build and tests') {
            steps {
                node(label: 'build') {
                    withMaven(maven: 'M3') {

                        // Run the maven build
                        sh "mvn clean install"

                    } // withMaven will discover the generated Maven artifacts, JUnit reports and FindBugs reports
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
                }

            }
        }
    }
}
