
# PPW1001

Tive a infelicidade de uma das minhas tomadas inteligentes parar de funcionar. Após análise do circuito, identifiquei que o problema não era físico e sim logico. Aí se iniciou uma busca pelo firmware do controlador WR2 da Tuya, mas infelizmente não encontrei em local algum.

Fui então forçado a remover a memória flash GD25Q16 e fazer um dump com uma programadora. O dump em questão é o tomadadefeito.bin , após conseguir fazer o dump com sucesso tentei reprogramar o chip para ver se aceitava gravação, após confirmar que era possível reprogramar pela programadora; Peguei outra tomada inteligente que estava em perfeito estado e fiz o mesmo processo de dump, o tomadabom.bin.

Com o dump da tomada que estava funcionando regravei a memória da tomada com defeito; Fiquei feliz ao ver que funcionou de primeira, comprovando que era o firmware que estava corrompido. Mas como eu fiz a clonagem do firmware todo, isto incluiu informações que deveriam ser diferentes, como serial e certificados de api. Desta maneira as duas tomadas funcionavam como se fosse o mesmo dispositivo.

Para resolver este inconveniente, voltei a analisar os firmwares e separei as diferenças entre eles, o diferenças.txt.

 Observei que nos primeiros 50 blocos, no firmware defeituoso, havia bits aleatórios, aparentando estarem corrompidos. E passando esses bits, havia uma quantidade grande de bits que eram idênticos em ambos os firmwares defeituoso e o bom. 
 
Por estarem no início do dump, supôs que eram informações de inicialização e por serem o mesmo hardware, também era o mesmo código. Isso explicava o motivo da tomada não ligar, pois o boot estava corrompido.

Considerando esses fatos, copiei os 50 blocos do firmware bom e sobre escrevi os 50 iniciais do firmware corrompido, regravei a memória e fiz os testes.

De fato, ela iniciou e conforme esperado, recuperou o serial de fábrica e o aplicativo enfim a identificou como uma tomada diferente.
Como não encontrei nenhum dump na internet, disponibilizo eles. Mas saliento que é necessário utilizar apenas a parte corrompida do dump, pois se utilizar o dump completo a tomada será um clone da minha.  No meu caso a parte que corrompeu é os 50 primeiros blocos.




[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit/)


