# DESAFIO DIO

def menu():
    menu = input("[1]DEPOSITO\n[2]SACAR\n[3]EXTRATO\n[4]NOVO USUARIO\n[5]NOVA CONTA\n[6]CONTAS\n[7]SAIR\n\n")
    return input(menu)

def deposito(saldo, valor,extrato,/):
    if valor > 0:
        saldo += valor
        print("Deposito feito com sucesso!")
        extrato += f"Deposito no valor de R${valor:.2f}........\n"
    else:
        print("Erro na operação, valor é invalido")
    
    return saldo, extrato

def sacar(*, saldo,valor,extrato,limite,qntd_saques, limites_saques):
    
    if valor > saldo:
        print("Operação falhou, valor maior que saldo")
        
    elif valor > limite:
        print("Operação falhou, ultrapassou o limite de R$ 500")
        
    elif qntd_saques > limites_saques:
        print("Operação falhou, ultrapassou limite de saques diarios")
        
    elif valor > 0 :
        saldo -= valor
        print("Valor sacado com sucesso!")
        extrato += f"Saque no valor de R${valor:.2f}........\n"
        qntd_saques +=1
        
    else:
        print("Operação falhou, Valor invalido!")
        
    return saldo,extrato
        
def mostrar_extrato(saldo,/,*, extrato):
    print("//////////////////////////////////////////\n")
    print("Não houveram transações." if not extrato else extrato)
    print(f"\nSaldo: R${saldo:.2f}")
    print("//////////////////////////////////////////\n")

def novo_usuario(usuarios):
    cpf = input("CPF(apenas numeros): ")
    usuario = filtrar_usuario(cpf,usuarios)
    
    if usuario:
        print("\n CPF já cadastrado")
        return
    
    nome = input("Nome completo: ")
    data_de_nascimento = input("Data de nascimento: ")
    endereco = input("Endereço: ")
    
    usuarios.append({"nome" : nome, "data_de_nascimeneto" : data_de_nascimento, "endereço" : endereco})
    print("Usuario criado!")
    
def filtrar_usuario(cpf,usuarios):
    usuarios_filtrados = [usuario for usuario in usuarios if usuario["cpf"] == cpf]
    return usuarios_filtrados[0] if usuarios_filtrados else None

def criar_conta(agencia, numero_conta,usuarios):
    cpf = input("CPF(apenas numeros): ")
    usuario = filtrar_usuario(cpf,usuarios)
    if usuario:
        print("\nConta criada!")
        return {"agencia" : agencia, "numero_conta" : numero_conta, "usuario" : usuario}
    
    print("Usuario não encontrado!")
        
def mostrar_contas(contas):
    for conta in contas:
        linha = f"""\
            Agencia:\t{conta["agencia"]}
            C/C:\t\t{conta["numero_conta"]}
            Titular:\t{conta["usuario"]["nome"]}
        """
        print("=" * 100)
        print(linha)
    
def main():
    LIMITE_SAQUES = 3
    AGENCIA = "0001"
    
    saldo = 0
    limite = 500
    extrato = " "
    qntd_saques = 0
    usuarios = [ ]
    contas = [ ]
    
    while True:
        opcao = menu()
        
        if opcao == 1:
            valor = float(input("Valor do deposito: "))
            saldo, extrato = deposito(saldo, valor, extrato)
            
        elif opcao == 2:
            valor = float(input("Valor do Saque: "))
            
            saldo, extrato = sacar( saldo = saldo, valor = valor, extrato = extrato, limite = limite, qntd_saques = qntd_saques, limite_saques = LIMITE_SAQUES)
            
        elif opcao == 3:
            mostrar_extrato(saldo, extrato = extrato)
            
        elif opcao == 4:
            novo_usuario(usuarios)
            
        elif opcao == 5:
            numero_conta = len(contas) + 1
            conta = criar_conta(AGENCIA, numero_conta, usuarios)
            
            if conta:
                contas.append(conta)
                
        elif opcao == 6:
            mostrar_contas(contas)
            
        elif opcao == 7:
            break
        
main() 
