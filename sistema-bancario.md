

saldo = 0
limite = 500
extrato = ""
quantidade_saque = 0 
LIMITE = 3
contador = 0 

while True:
    opcao = int(input("[1] Depositar\n[2] Sacar\n[3] Extrato\n[4] Sair\n\n"))
    
    if opcao == 1:
        valor = int(input("Valor a ser depositado: "))
        saldo += valor
        print("\nValor depositado com sucesso\n")
        extrato += (f"Deposito no valor de: R$ {valor}")
        
    elif opcao == 2:
        contador +=1
        
        if contador > LIMITE:
            print("Você atingiu o limite diario\n")
            break
        
        saque = int(input("Valor a ser sacado: \n"))
        
        if saque > saldo or saque > 500:
            print("Saldo indisponivel ou Valor excede o limite de R$ 500 por saque\n")
            break
        
        saldo -= saque
        
        extrato += (f"\nVoce realizou um saque de: R$ {saque}...\n")
        
        print("Saque realizado com sucesso\n")
        
    elif opcao == 3:
        print(extrato)
        print(f"\nSaldo disponivel na conta é de: R$ {saldo}\n")
        
    elif opcao == 4:
        print("Saindo do sistema....")
        break
        
    else:
        print("Operação invalida, Tente novamente\n")
    
            
        
        
       
            
        
