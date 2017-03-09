pipeline {
    agent none
    stages {
        stage('build and tests') {
            steps {
                node(label: 'build') {
                    sleep '5'
                }

            }
        }
        stage('static-analysis') {
            steps {
                node(label: 'build') {
                    sleep '5'
                }

            }
        }
        stage('acceptance-test') {
            steps {
                parallel(
                        "edge": {
                            node(label: 'build') {
                                sleep '5'
                            }


                        },
                        "chrome": {
                            node(label: 'build') {
                                sleep '5'
                            }


                        },
                        "firefox": {
                            node(label: 'build') {
                                sleep '5'
                            }


                        }
                )
            }
        }
        stage('staging') {
            steps {
                node(label: 'build') {
                    sleep '5'
                }

            }
        }
        stage('manual-approval') {
            steps {
                input 'Déploiement en Prod ?'
            }
        }
        stage('deploy') {
            steps {
                node(label: 'build') {
                    sleep '5'
                    echo 'Fini !!!'
                }

            }
        }
    }
}
