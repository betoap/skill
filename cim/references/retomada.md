# Retomada e retornos

Ao receber uma solicitação para retomar um ciclo, localize primeiro seu identificador e reconcilie o estado da CIM com os handoffs de SIM, FIO e DIO. Retome somente no último nó cujo conjunto de entradas esteja completo, atual e aderente ao contrato.

Quando um handoff for invalidado, registre o motivo, preserve o histórico e retorne apenas à skill produtora ou à etapa que precisa de esclarecimento. Não reinicie SIM, FIO ou DIO por conveniência e não converta um resultado parcial em confirmação.
