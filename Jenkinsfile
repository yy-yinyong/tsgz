pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh '''cd /home/yinyong

rm -rf webinner;
svn co https://172.16.0.58:7777/svn/bigdata/tsgz/web/trunk/modules/webinner


cd /home/yinyong/webinner
sh module_build.sh


file=$(find /home/yinyong/webinner -name *.tar.gz)

cd /home/yinyong
./sshpass -p bigdata@92 scp -o StrictHostKeyChecking=no /home/yinyong/webinner/${file##*/} root@172.16.3.92:/home/yinyong

'''
      }
    }

    stage('Install') {
      steps {
        sh '''cd /home/yinyong
./sshpass -p bigdata@92 ssh root@172.16.3.92


file=$(find /home/yinyong -name tsgz*.tar.gz)

cd /home/yinyong
rm -rf tsgz-webinner-install
tar -xzvf ${file##*/}

cd tsgz-webinner-install
./module_install.sh install

exit
exit'''
      }
    }

  }
}