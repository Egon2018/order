pipeline {
  agent any
  stages {
    stage('checkout') {
      steps {
        git(url: 'https://github.com/Egon2018/order.git', branch: 'master', changelog: true)
      }
    }
    stage('sleep') {
      steps {
        sleep 30
      }
    }
    stage('bulid') {
      steps {
        sh '''cd /var/lib/jenkins/order-mastar
mvn clean install'''
      }
    }
    stage('start tomcat') {
      steps {
        sh '''export ENV=DEV  
export DEPLOYMENT_HOME=/var/lib/jenkins/workspace/order_master  
export USERPORTAL_HOME=/home/tomcat-8010

  
echo "[Deploy] Shutting down 8010"  
if [ `ps auxwwww|grep tomcat-8010|grep -v grep|wc -l` -gt 0 ]  
then  
for pid in `ps auxwww|grep tomcat-8010|grep -v grep|tr -s \' \'|cut -d \' \' -f2`  
do  
kill -9 $pid 2>&1 > /dev/null  
done  
fi  
  
  
echo "[Deploy] Cleaning cache for 8010"  
rm -rf $USERPORTAL_HOME/work/Catalina/localhost/*  
echo "[Deploy] Removing 8010.war"  
rm -rf $USERPORTAL_HOME/webapps/*  
  
echo "[Deploy] Copying new 8010.war"  
cp $DEPLOYMENT_HOME/target/order.war $USERPORTAL_HOME/webapps/  
  
  
echo "[Deploy] Starting up 8010"  
$USERPORTAL_HOME/bin/startup.sh  '''
      }
    }
  }
  environment {
    branch = 'master'
  }
}