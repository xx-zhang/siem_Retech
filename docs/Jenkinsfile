pipeline {
  agent {
      node {
          label 'centos7-jdk11-devops'
      }
  }

  environment {
	  RELEASE_SITE_DIR = "https://10.7.202.199/filestore/ngx-deps/"
      BUILD_COMP_TAG = "websrv-xc.x84_64"
  }

  options {
	  parallelsAlwaysFailFast()
  }

//    options {
//       buildDiscarder logRotator(
//         daysToKeepStr: '16',
//         numToKeepStr: '10'
//       )
//    }

  stages {
    stage("分支检出") {
      steps {

        echo 'checkout all branch Jenkinsfile'
        checkout([
            $class: 'GitSCM',
            branches: [[name: '*/tongsuo']],
            userRemoteConfigs: [[url: 'http://10.7.202.171:10880/superman/nginx-bdwaf.git']]
        ])

      }
    }

    stage('环境测试') {
      parallel {

        stage('1. 更新YUM源的准备') {
          steps {
            script {
              sh 'uname -a'
              // sh "sed -i 's/\r//' ./auxil/rhel7_prepare.sh && bash ./auxil/rhel7_prepare.sh"
              sh 'curl -SL '
            }
          }
        }

        stage('测试环境变量OK') {
          when {
            branch 'dev'
            environment name: 'DOCKER_IMAGE_TAG', value: 'dev'
          }
        steps {
            script {
              sh "echo 1"
              sh "echo 22"
              sh "echo 333"
            }
          }
        }

      }
    }

	stage('测试远程仓库OK') {
    steps {
		   // 连续登录三次，看看能不能授权成功，有时候网络容易卡。
	    retry(3) {
            sleep(5)
            timeout(time: 3, unit: "SECONDS") {
//             sh "docker login ${DOCKER_REGISTRY_HOSTNAME} -u ${DOCKER_REGISTRY_USERNAME}  -p ${DOCKER_REGISTRY_CREDENTIAL}"
               sh "if [ `curl -s https://10.7.202.199/filestore/ -o /dev/null -k -w '%{http_code}' --connect-timeout 1` -eq '200' ]; then echo 'Connect OK...'; else echo '[x] Connect Error';  fi"
          }
        }
      }
    }

    stage('构建组件包') {
      steps {
        // 确保仓库中有可用的 Dockerfile
        sh "yum -y install devtoolset-7"
        sh "scl enable devtoolset-7 bash"
        sh "sed -i 's/\r//' ./modsecurity.sh && bash ./modsecurity.sh"
      }
    }

    stage('构建后的操作') {
      steps {
        // 推送镜像到远程仓库
        sh "rm -rf ./nginx/conf/ && /usr/bin/cp -r ./conf/ ./nginx/"
        sh "rm -rf ./nginx/html/ && /usr/bin/cp -r ./html/ ./nginx/"
        sh "/usr/bin/cp ./nginx.sh ./nginx/"
        sh "sed -i 's/\r//' ./nginx/nginx.sh && chmod u+x ./nginx/nginx.sh"

      }
    }


  }

  post {
        always {
            echo "Topsec BigData Licence v1 For BdTech. IC"
        }
    }

}
