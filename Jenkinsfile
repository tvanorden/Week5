podTemplate(containers: [
containerTemplate(
name: 'gradle',
image: 'gradle:6.3-jdk14',
command: 'sleep',
args: '30d'
),
]) {
node(POD_LABEL) {
stage('Run pipeline against a gradle project') {
git 'https://github.com/tvanorden/Continuous-Delivery-with-Docker-and-Jenkins-Second-Edition.git'
container('gradle') {
stage('Build a gradle project') {
sh '''
cd Chapter08/sample1
chmod +x gradlew
./gradlew test
'''
}


stage("Code coverage") {
try {
sh '''
pwd
cd Chapter08/sample1
./gradlew jacocoTestCoverageVerification
./gradlew jacocoTestReport
'''
} catch (Exception E) {
echo 'Failure detected'
}
publishHTML (target: [
reportDir: 'Chapter08/sample1/build/reports/jacoco/test/html',
reportFiles: 'index.html',
reportName: "JaCoCo Report"
])







stage("Static code analysis") {
try {

sh '''
pwd
cd Chapter08/sample1
./gradlew checkstyleMain
'''


}


catch (Exception E) {
echo 'Failure detected'
}


publishHTML (target: [
reportDir: 'Chapter08/sample1/build/reports/checkstyle/',
reportFiles: 'main.html',
reportName: "JaCoCo checkstyle"
])






}

}
}
}
}
}
