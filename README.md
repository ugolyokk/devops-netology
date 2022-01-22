# devops-netology
#Будут проигнорироаны файлы в имени которых есть:
	*.tfstate
	*.tfstate.*
	override.tf
	override.tf.json
	*_override.tf
	*_override.tf.json

	#Файлы логов
	crash.log
	crash.*.log

	#Файлы вкоторых могут содержать конфиденциальную информацию
	*.tfvars

	#Некие конфигурационные файлы
	.terraformrc
	terraform.rc
