# state-machine
State machine template that use enum (state machine in C#, example for Unity 3D)

## how to use
- create an enum list for states
```
public enum GameState
{
    MainMenu,
    GameMenu,
    InGame,
    Restarting,
    Exiting, 
}
```

- create an enum list for commands (commands are used as events for transitions)
```
public enum GameCommand
{
    Start,
    Back
}
```

- create a class for your specific state machine that inherits StateMachine class, whit the enum as parameters of the template
```
public class GameStateMachine : StateMachine<GameState, GameCommand>
```

- implement a constructor for your state machine that use base constructor with your initial state as parameter, and add transitions (defined by the current state, the command and the next state)
```
public GameStateMachine() : base(GameState.InGame)
{
    transitions.Add(new StateTransition<GameState, GameCommand>     (GameState.MainMenu,    GameCommand.Start), GameState.InGame);
    [...]
}
```

- you can now use your custom state machine : GetNext(Command) is used for determining which state would be the next using a command on the current state, MoveNext(Command) is used to perform the transition
```
public GameStateMachine gameStateMachine = new GameStateMachine();

void Update
{
    UpdateStateMachine();
    
    if (gameStateMachine.currentState == GameState.MainMenu)
        Debug.Log("MainMenuLoop");
    if (gameStateMachine.currentState == GameState.InGame)
        Debug.Log("InGameLoop");
    [...]
}

void UpdateStateMachine()
{
    if (input_start)
        gameStateMachine.MoveNext(GameCommand.Start);

    if (input_back)
        gameStateMachine.MoveNext(GameCommand.Back);
}
```
