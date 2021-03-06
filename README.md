# VK_PHP_test_task

Chess game back-end as VK Test task for internship program


Все команды в API передаются через POST-запрос

Структура запроса:

 - game -- массив, содержащий все сведения о текущей игре (объект класса Game в коде)
 - одна из следующих команд:
    - new -- начало новой игры. 1 -- если нужно начать. Если не нужно начинать, метод не используется
    - possibleMoves -- получение возможных ходов для конкретного состояния игры. Передаются лишь две координаты фигуры в формате (x,y), где x и y -- числа от 1 до 8
    - move -- метод перемещения фигуры. На вход подаются:
      - начальные координаты фигуры (см. possibleMoves) в массиве
      - массив доступных ходов (генерируется в результате метода possibleMoves)
      - направление (две координаты), тип хода (простой или рокировка), тип фигуры (так как пешка может превратиться в другую фигуру) в массиве
   - reset -- перезапускает текущую игру и возвращает новый объект класса Game
   - getMoveLog -- возвращает массив лога движений. Формат элемента лога -- отправная точка фигуры; точка, куда она переместилась; её цвет(для идентификации игрока)

Ответом на любой запрос является JSON-строка с массивом answer, состоящим из элемента RESULT. Если его значение отрицательное, то значит, что произошла одна из ошибок:

 - -1 -- ошибка о том, что методу подана пустая игра
 - -2 -- ошибка о том, что совершен неправильный ход.
 - -3 -- ошибка о том, что методу подан пустой массив возможных ходов

Если значение answer['RESULT'] равно положительному числу, то получился выигрыш одного из игроков:
-  1 -- выиграл черный игрок
 - 2 -- выиграл белый игрок
  
Иначе значение данного элемента -- либо массив объекта game, либо массив с ходами, либо массив с логом ходов.

Репозиторий стостоит из трех основных файлов:
- Game.php -- Это класс, отвечающий за саму игру и содержащий все сведения о ней, в том числе и состояние доски
- Figure.php -- Это класс для фигур шахматной доски
- api.php -- Это файл, в котором простенькое апи, взаимодействующее с программой и пользователем.
