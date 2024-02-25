properties([
    parameters([
        choice(
            name: 'typeParam',
            choices: [
                'Integer Squares',
                'Non-Integer Squares'
            ]
        ),
        [$class: 'CascadeChoiceParameter',
            choiceType: 'PT_SINGLE_SELECT',
            description: 'Choose numbers',
            filterLength: 1,
            filterable: false,
            name: 'integer_squares_param',
            referencedParameters: 'typeParam',
            script: [
                $class: 'GroovyScript',
                script: [
                    classpath: [],
                    sandbox: true,
                    script: """
                        def type = typeParam
                        if (type == 'Integer Squares') {
                            return ['36', '64', '81']
                        } else {
                            return ['13', '15', '21', '23', '45', '46', '64', '66']
                        }
                    """
                ]
            ]
        ]
    ])
])
pipeline {
    agent any
    stages {
        stage('Square Root') {
            steps {
                script {
                    try {
                        def type = params.typeParam
                        def number = params.integer_squares_param
                        double parsedNumber = Double.parseDouble(number)

                        if (type == 'Integer Squares' && !(parsedNumber % 1 == 0)) {
                            throw new Exception("Выбрано неверное значение для типа 'Integer Squares'")
                        } else if (type == 'Non-Integer Squares' && parsedNumber % 1 == 0) {
                            throw new Exception("Выбрано неверное значение для типа 'Non-Integer Squares'")
                        }

                        double result = Math.sqrt(parsedNumber)
                        echo "Корень из ${number} равен ${result}"
                    } catch (Exception e) {
                        echo "Ошибка: ${e.message}"
                    }
                }
            }
        }
    }
}
