<template>
<div class="grid">
    <div class="col-12">
        <div class="card">
             <Timeline :value="events" align="left"  style="maxWidth: 1px;, paddingLeft: 0px;, paddingRight: 0px;">
                <template #marker="slotProps">
                <span class="flex w-2rem h-2rem align-items-center justify-content-center text-white border-circle z-1 shadow-2" :style="{backgroundColor: slotProps.item.color}">
                    
                </span>
                </template>
                <template #content="slotProps">
                    <Card style="width:780px;">
                        <template #title>
                            {{slotProps.item.status}}
                        </template>
                        <template #subtitle>
                            {{slotProps.item.date}}
                        </template>
                        <template #content>
                            <Accordion>
                                <AccordionTab v-for="tab in tabs" :key="tab.title" :header="tab.title">
                                    
                                    <img v-if="slotProps.item.image" :src="'images/product/' + slotProps.item.image" :alt="slotProps.item.name"  class="shadow-2 mb-3" />
                                    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Inventore sed consequuntur error </p>
                                    <Button label="Read more" class="p-button-text"></Button>
                                </AccordionTab>
                            </Accordion>
                            
                        </template>
                    </Card>
                </template>
            </Timeline>
        </div>
    </div>
   
</div>

</template>

<script>
export default {
    data() {
        return {
           
            events: [
                {status: 'CLIENTE', date: '15/10/2020 10:30', icon: 'pi pi-shopping-cart', color: 'blue', image: 'game-controller.jpg'},
                {status: 'DETALLES', date: '15/10/2020 14:00', icon: 'pi pi-cog', color: 'blue'},
                {status: 'EXPEDIENTE', date: '15/10/2020 16:15', icon: 'pi pi-shopping-cart', color: 'blue'},
                {status: 'TRÁMITE', date: '16/10/2020 10:00', icon: 'pi pi-check', color: 'green'}
            ],
            tabs: [
				{title: 'Ver más', content: 'Content 1'}
			]
        }
    }
}
</script>

<style  scoped>

</style>

