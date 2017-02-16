#!groovy

node {
    stage "Checkout"
    checkout scm

    def contribBranch = env.BRANCH_NAME.replaceAll('-base', '')
    stage "Checkout contrib modules"
    sh "rm -Rf policy/modules/contrib"
    sh "git clone -b ${contribBranch} https://github.com/fedora-selinux/selinux-policy-contrib.git"

    stage "Configure"
    echo "Configuring policy build for ${env.BRANCH_NAME}"
    sh "make conf"

    stage "Documentation"
    echo "Generating documentation"
    sh "make html"

    publishHTML (target: [
        allowMissing: false,
        alwaysLinkToLastBuild: false,
        keepAll: true,
        reportDir: 'doc/html',
        reportFiles: 'index.html',
        reportName: "Policy Documentation"
    ])
}
