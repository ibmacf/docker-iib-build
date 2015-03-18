#
IIBADMIN =iibadm
IIBNODE = NSW
IIBCONFIGDIR = /home/ashley/IBMDEMO/iib-10.0.710.0/build/configuration/NSW/barfiles
CMD = "su - ${IIBADMIN} -c"

.PHONY: createnode createis configurenode

deletenode:
	su - ${IIBADMIN} -c "mqsistop $(IIBNODE)"
	su - ${IIBADMIN} -c "mqsideletebroker $(IIBNODE)"

createnode:
	su - ${IIBADMIN} -c "mqsicreatebroker $(IIBNODE)"
	su - ${IIBADMIN} -c "mqsistart $(IIBNODE)"	
	echo user $(IIBADMIN) >> /var/mqsi/components/${IIBNODE}/config/${IIBNODE}

createis: createnode 
	su - ${IIBADMIN} -c "mqsicreateexecutiongroup $(IIBNODE) -e OATLEY"
	su - ${IIBADMIN} -c "mqsicreateexecutiongroup $(IIBNODE) -e PANANIA"
	su - ${IIBADMIN} -c "mqsicreateexecutiongroup $(IIBNODE) -e NARAABEAN"

configurenode: createis
	cd $(IIBCONFIGDIR)
	su - ${IIBADMIN} -c "mqsideploy $(IIBNODE) -e OATLEY -a ../barfiles/echoService.bar"