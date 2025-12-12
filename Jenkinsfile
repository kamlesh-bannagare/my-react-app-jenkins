node {
    def appDir = '/var/www/nextjs-app'

    stage('Clean Workspace'){
        echo 'Cleaning Jenkins Workspace'
        deleteDir()
    }

    stage('Clone Repo'){
        echo 'Cloning the repoo'

        git(
            branch: 'main',
            url: 'https://github.com/kamlesh-bannagare/careerj-vite-frontend'
        )
    }

    stage('Deploy to EC2'){
        echo 'Deploying to EC2 AWSs'

        sh """

            sudo mkdir -p ${appDir}
            sudo chown -R jenkins:jenkins ${appDir}

            rsync -av --delete --exclude='.git' --exclude='node_modules' . ${appDir}

            cd ${appDir}
            # FIX
            sudo rm -rf node_modules
            sudo rm -f package-lock.json
            sudo npm install
            sudo npm run build
            sudo fuser -k 3000/tcp || 
            true
            npm run dev
        """
    }
}