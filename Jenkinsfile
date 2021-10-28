pipeline{
   agent any
   
   stages{
      stage('Checkout Stage'){
	     steps{
		    echo 'Data is fetched successfully from github.com'
		 }
   }
   
    stage('Docker build Stage'){
	     steps{
		    sh 'docker build -t testapp .'
			echo 'Docker build stage successfully excuted'
		 }
    }
   
    stage('Approval Step'){
            steps{
                
                //----------------send an approval prompt-------------
                script {
                   env.APPROVED_PUSH = input message: 'Please enter input',
                   parameters: [choice(name: 'Deploy?', choices: 'no\nyes', description: 'Choose "yes" if you want to deploy this build')]
                       }
                //-----------------end approval prompt------------
            }
    }
   
    stage('Docker push stage'){
	     when {
                environment name:'APPROVED_PUSH', value: 'yes'
         }
	     steps{
		    
		    sh 'docker push nanditasahu/testapp'
		 }
   }
   }
   
   post{
      success{
	     echo 'Successfully excuted'
	  }
	  
	  failure{
	     echo 'Fail....Please check again!!'
	  }
   }
}
