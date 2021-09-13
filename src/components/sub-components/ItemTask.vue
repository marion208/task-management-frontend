<template>
    <div class="card_item" :id="'containertask' + idtask">
        <div class="container_space_between">
            <div class="status_container" :id="containerstatustask$idtask">
                <span :class="'statustask' + idstatustask + ' mouse-pointer'" title="Changer le statut" :id="'statustask' + idtask" @click="updateStatusTask(idtask)">{{ namestatustask }}</span>
            </div>
        </div>
    </div>
</template>

