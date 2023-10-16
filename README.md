options:
  coins:
    type: map
    default: { }

command: /coin add <number>
    permission: admin.permission
    executable by: players
    usage: /coin add <number>
    trigger:
        set {_amount} to arg-1
        add {_amount} to player's coins
        send "You now have %{player's coins::%} coins."

command /checkcoins:
    executable by: players
    trigger:
        send "You have %{player's coins::%} coins."
        
