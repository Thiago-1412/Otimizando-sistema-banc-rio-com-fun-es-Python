# Otimizando-sistema-bancario-com-funçoes-Python

def depositar(saldo, extrato, valor):
    if valor > 0:
        saldo += valor
        extrato += f"Depósito: R$ {valor:.2f}\n"
        print("Depósito realizado com sucesso.")
    else:
        print("Operação falhou! O valor informado é inválido.")
    return saldo, extrato
 
def sacar(saldo, extrato, valor, limite, numero_saques, LIMITE_SAQUES):
    if valor > saldo:
        print("Operação falhou! Você não tem saldo suficiente.")
    elif valor > limite:
        print("Operação falhou! O valor do saque excede o limite.")
    elif numero_saques >= LIMITE_SAQUES:
        print("Operação falhou! Número máximo de saques excedido.")
    elif valor > 0:
        saldo -= valor
        extrato += f"Saque: R$ {valor:.2f}\n"
        numero_saques += 1
        print("Saque realizado com sucesso.")
    else:
        print("Operação falhou! O valor informado é inválido.")
    return saldo, extrato, numero_saques
 
def exibir_extrato(saldo, extrato):
    print("\n================ EXTRATO ================")
    print("Não foram realizadas movimentações." if not extrato else extrato)
    print(f"\nSaldo: R$ {saldo:.2f}")
    print("==========================================")
 
def menu():
    saldo = 0
    limite = 500
    extrato = ""
    numero_saques = 0
    LIMITE_SAQUES = 3
    while True:
        opcao = input("\n[d] Depositar\n[s] Sacar\n[e] Extrato\n[q] Sair\n\n=> ")
 
        if opcao == "d":
            valor = float(input("Informe o valor do depósito: "))
            saldo, extrato = depositar(saldo, extrato, valor)
 
        elif opcao == "s":
            valor = float(input("Informe o valor do saque: "))
            saldo, extrato, numero_saques = sacar(saldo, extrato, valor, limite, numero_saques, LIMITE_SAQUES)
 
        elif opcao == "e":
            exibir_extrato(saldo, extrato)
 
        elif opcao == "q":
            print("Saindo do sistema.")
            break
 
        else:
            print("Operação inválida, por favor selecione novamente a operação desejada.")
 
menu()
