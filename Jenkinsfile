pipeline {
    agent any

    parameters {
        // Active Choice параметр
        choice(
            name: 'typeParam',
            choices: ['Integer Squares', 'Non-Integer Squares'],
            description: 'Choose type of numbers'
        )
    }

    stages {
        stage('Square Root') {
            steps {
                script {
                    try {
                        def type = params.typeParam
                        def number
                        // Получаем значение в зависимости от выбранного типа параметра
                        if (type == 'Integer Squares') {
                            // Dynamic Reference параметр для Integer Squares
                            number = params.integer_squares_param
                        } else {
                            // Dynamic Reference параметр для Non-Integer Squares
                            number = params.non_integer_squares_param
                        }
                        
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
