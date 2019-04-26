node('master') {
	try{
			
		stage('Checkout ') {
		 	git 'https://github.com/argaurava/DevOps-Demo-Project.git'
		}

		stage('Build Automation') {    
			sh 'mvn clean package'
		}
		
		
		dir(/root/DevOpsProject/Terr/Terraform) {
			stage('Infa Creation'){
				sh "/usr/local/bin/terraform apply -auto-approve -var-file=../modulone.tfvars"
				sh "terraform output aws_instance_public_ip > /root/DevOpsProject/Ansible/aws_dns_name.txt"
			}
		}
		
		dir(/root/DevOpsProject/Ansible) {
			stage('Ansible Configuration'){
				sh "/root/Ansible/create_inv.sh"
				sh "/usr/bin/ansible-playbook -i invertory.ini site.yml"
			}
		}
	}
	catch(err) {
		notify("Error ${err}")
		currentBuild.result='FAILURE'
	}

}
