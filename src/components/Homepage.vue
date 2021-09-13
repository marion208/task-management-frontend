<template>
    <div>
    <h2 class="title">Application de gestion de tâches</h2>
    <div class="big_button_container">
      <div class="big_button_div">
        <span class="big_button mouse-pointer" @click="showInputNewList">
        <svg height="1em" width="1em" version="1.1" id="Capa_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 512 512" style="enable-background:new 0 0 512 512;" xml:space="preserve"><g><g><path d="M256,0C114.833,0,0,114.833,0,256s114.833,256,256,256s256-114.853,256-256S397.167,0,256,0z M256,472.341 c-119.275,0-216.341-97.046-216.341-216.341S136.725,39.659,256,39.659S472.341,136.705,472.341,256S375.295,472.341,256,472.341z"/></g></g><g><g><path d="M355.148,234.386H275.83v-79.318c0-10.946-8.864-19.83-19.83-19.83s-19.83,8.884-19.83,19.83v79.318h-79.318 c-10.966,0-19.83,8.884-19.83,19.83s8.864,19.83,19.83,19.83h79.318v79.318c0,10.946,8.864,19.83,19.83,19.83 s19.83-8.884,19.83-19.83v-79.318h79.318c10.966,0,19.83-8.884,19.83-19.83S366.114,234.386,355.148,234.386z"/></g></g></svg>Ajouter une nouvelle liste</span>
        <div class="hiddennewlistinput" id="newlist">
          <input id="inputlist" type="text" maxlength="255"/>
          <label title="Valider" class="mouse-pointer" @click="addNewList">
            <svg height="1em" viewBox="-59 0 512 512" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="m344.675781 39.398438h-48.671875v-19.398438c0-11.046875-8.953125-20-20-20h-157.339844c-11.046874 0-20 8.953125-20 20v19.398438h-48.664062c-27.570312 0-50 22.429687-50 50v372.601562c0 27.570312 22.429688 50 50 50h294.675781c27.570313 0 50-22.429688 50-50v-372.601562c0-27.570313-22.433593-50-50-50zm-88.671875.601562v38.800781h-117.34375c0-13.292969 0-24.273437 0-38.800781zm98.671875 422c0 5.515625-4.488281 10-10 10h-294.675781c-5.515625 0-10-4.484375-10-10v-372.601562c0-5.511719 4.484375-10 10-10h48.660156v19.402343c0 11.046875 8.957032 20 20 20h157.34375c11.042969 0 20-8.953125 20-20v-19.402343h48.671875c5.511719 0 10 4.488281 10 10zm-64.535156-228.480469c7.8125 7.8125 7.8125 20.476563 0 28.285157l-105.101563 105.101562c-7.808593 7.8125-20.472656 7.8125-28.285156 0l-52.230468-52.230469c-7.808594-7.808593-7.808594-20.472656 0-28.285156 7.8125-7.808594 20.472656-7.808594 28.285156 0l38.089844 38.089844 90.957031-90.957031c7.8125-7.8125 20.472656-7.8125 28.285156-.003907zm0 0"/></svg>
          </label>
        </div>
      </div>
    </div>
    <div>
      <p>
      </p>
    </div>
    <div class="card_container" id="card_container">
      <template v-for="oneList in taskslists">
          <div class="card" v-bind:key="oneList.id" :id="'card' + oneList.id_list">
              <div class="container_space_between">
                <div>
                  <span class="card_title" :id="'titlelist' + oneList.id_list">
                    {{ oneList.name_list }}
                  </span>
                  <span v-if="oneList.nb_tasks_total > 0" :id="'progressionlist' + oneList.id_list">
                    ({{ (oneList.nb_tasks_completed * 100 / oneList.nb_tasks_total).toFixed(0) }}%)&nbsp;
                  </span>
                  <span v-else :id="'progressionlist' + oneList.id_list">
                    (0%)&nbsp;
                  </span>
                </div>
                <div>
                  <buttonUpdate v-on:click.native="showUpdateList(oneList.id_list)"></buttonUpdate>
                  <buttonDelete v-on:click.native="deleteList(oneList.id_list)"></buttonDelete>
                </div>
              </div>
              <div class="hiddenupdatelist" :id="'updatelist' + oneList.id_list">
                <input :id="'inputupdatelist' + oneList.id_list" type="text" maxlength="255"/>
                <label title="Valider" class="mouse-pointer" @click="updateNameList(oneList.id_list)">
                  <svg height="1em" viewBox="-59 0 512 512" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="m344.675781 39.398438h-48.671875v-19.398438c0-11.046875-8.953125-20-20-20h-157.339844c-11.046874 0-20 8.953125-20 20v19.398438h-48.664062c-27.570312 0-50 22.429687-50 50v372.601562c0 27.570312 22.429688 50 50 50h294.675781c27.570313 0 50-22.429688 50-50v-372.601562c0-27.570313-22.433593-50-50-50zm-88.671875.601562v38.800781h-117.34375c0-13.292969 0-24.273437 0-38.800781zm98.671875 422c0 5.515625-4.488281 10-10 10h-294.675781c-5.515625 0-10-4.484375-10-10v-372.601562c0-5.511719 4.484375-10 10-10h48.660156v19.402343c0 11.046875 8.957032 20 20 20h157.34375c11.042969 0 20-8.953125 20-20v-19.402343h48.671875c5.511719 0 10 4.488281 10 10zm-64.535156-228.480469c7.8125 7.8125 7.8125 20.476563 0 28.285157l-105.101563 105.101562c-7.808593 7.8125-20.472656 7.8125-28.285156 0l-52.230468-52.230469c-7.808594-7.808593-7.808594-20.472656 0-28.285156 7.8125-7.808594 20.472656-7.808594 28.285156 0l38.089844 38.089844 90.957031-90.957031c7.8125-7.8125 20.472656-7.8125 28.285156-.003907zm0 0"/></svg>
                </label>
              </div>
              <template v-for="oneTask in oneList.tasks">
                <div class="card_item" v-bind:key="'containertask' + oneTask.id_task" :id="'containertask' + oneTask.id_task">
                  <div class="container_space_between">
                    <div class="status_container" :id="'containerstatustask' + oneTask.id_task">
                      <statusTask :class="'statustask' + oneTask.id_status_task + ' mouse-pointer'" :id="'statustask' + oneTask.id_task" v-on:click.native="updateStatusTask(oneTask.id_task)" v-html="oneTask.name_status_task"></statusTask>
                    </div>
                    <div>
                      <buttonUpdate v-on:click.native="showUpdateTask(oneTask.id_task)"></buttonUpdate>
                      <buttonDelete v-on:click.native="deleteTask(oneTask.id_task)"></buttonDelete>
                    </div>
                  </div>
                  <div class="input_new_task_container">
                    <div class="hiddenupdatetaskinput" :id="'updatetask' + oneTask.id_task">
                      <input :id="'inputupdatetask' + oneTask.id_task" type="text" maxlength="255"/>
                      <buttonValidate v-on:click.native="updateNameTask(oneTask.id_task)"></buttonValidate>
                    </div>
                  </div>
                  <div>
                    <span class="small_padding_right" :id="'nametask' + oneTask.id_task">{{ oneTask.name_task }}</span>
                  </div> 
                </div>
              </template>
              <div class="input_new_task_container">
                <buttonAddTask v-on:click.native="showInputNewTask(oneList.id_list)"></buttonAddTask>
              </div>
              <div class="input_new_task_container">
                <div class="hiddennewtaskinput" :id="'newtasklist' + oneList.id_list">
                  <input :id="'inputtask' + oneList.id_list" type="text" maxlength="255"/>
                  <buttonValidate v-on:click.native="addNewTask(oneList.id_list)"></buttonValidate>
                </div>
              </div>
          </div>
      </template>
      </div>
      <footer>
            <p><strong>Mentions légales :</strong><br/>
            Ce site ne collecte ni cookie ni donnée personnelle.<br/>
            Site hébergé par <a href="https://www.ionos.com/">IONOS</a></p>
      </footer>
    
  </div>
</template>

<script>
import axios from 'axios';
/*import taskitem from './sub-components/ItemTask';*/
import statusTask from './sub-components/TasksStatus';
import buttonUpdate from './buttons/ButtonUpdate';
import buttonDelete from './buttons/ButtonDelete';
import buttonValidate from './buttons/ButtonValidate';
import buttonAddTask from './buttons/ButtonAddTask';

export default {
  name: 'Homepage',
  components: {
    /*taskitem,*/
    statusTask,
    buttonUpdate,
    buttonDelete,
    buttonValidate,
    buttonAddTask
  },
  data() {
    return {
      taskslists: [],
      currentnumlist: 0,
      currentnumtask: 0
    }
  },
  methods: {
        showInputNewList: function () {
          var el = document.getElementById('newlist');
          if (el.classList == "hiddennewlistinput") {
            el.classList.remove("hiddennewlistinput");
            el.classList.add("showednewlistinput");
          } else {
            el.classList.remove("showednewlistinput");
            el.classList.add("hiddennewlistinput");
          }
        },
        showInputNewTask: function (numlist) {
          var el = document.getElementById('newtasklist'+numlist);
          if (el.classList == "hiddennewtaskinput") {
            el.classList.remove("hiddennewtaskinput");
            el.classList.add("showednewtaskinput");
          } else {
            el.classList.remove("showednewtaskinput");
            el.classList.add("hiddennewtaskinput");
          }
        },
        showUpdateList: function(numlist) {
          var el = document.getElementById('updatelist'+numlist);
          if (el.classList == "hiddenupdatelist") {
            el.classList.remove("hiddenupdatelist");
            el.classList.add("showedupdatelist");
            var eltitle = document.getElementById('titlelist'+numlist);
            var title = eltitle.innerHTML.trim();
            document.getElementById('inputupdatelist'+numlist).value = title;
          } else {
            el.classList.remove("showedupdatelist");
            el.classList.add("hiddenupdatelist");
          }
        },
        showUpdateTask: function(numtask) {
          var el = document.getElementById('updatetask'+numtask);
          if (el.classList == "hiddenupdatetaskinput") {
            el.classList.remove("hiddenupdatetaskinput");
            el.classList.add("showedupdatetaskinput");
            var elname = document.getElementById('nametask'+numtask);
            var name = elname.innerHTML.trim();
            document.getElementById('inputupdatetask'+numtask).value = name;
          } else {
            el.classList.remove("showedupdatetaskinput");
            el.classList.add("hiddenupdatetaskinput");
          }
        },
        addNewList: function () {
          var el = document.getElementById('inputlist');
          var inputtext = el.value;

          var newList = [{
                "namelist": inputtext
          }];
          var jsonNewList = JSON.stringify(newList);
          axios.post(process.env.VUE_APP_API_URL + '/addList', jsonNewList)
            .then(() => {
              var el = document.getElementById('newlist');
              el.classList.remove("showednewlistinput");
              el.classList.add("hiddennewlistinput");
              axios.get(process.env.VUE_APP_API_URL + '/listsoftaskslists')
                    .then(response => (this.taskslists = response.data));
                });
        },
        addNewTask: function (numlist) {
          var el = document.getElementById('inputtask'+numlist);
          var inputtext = el.value;

          var newTask = [{
                "idlist": numlist,
                "nametask": inputtext
          }];
          var jsonNewTask = JSON.stringify(newTask);
          axios.post(process.env.VUE_APP_API_URL + '/addTask', jsonNewTask)
             .then(response => {
              this.currentnumtask = response.data['idtask'];
              var el = document.getElementById('newtasklist'+numlist);
              el.classList.remove("showednewtaskinput");
              el.classList.add("hiddennewtaskinput");
              axios.get(process.env.VUE_APP_API_URL + '/listsoftaskslists')
                .then(response => (this.taskslists = response.data));
             });
        },
        updateNameList: function(numlist) {
          var el = document.getElementById('inputupdatelist'+numlist);
          var inputtext = el.value;

          var updateNameList = [{
                "idlist": numlist,
                "namelist": inputtext
          }];
          var jsonUpdateNameList = JSON.stringify(updateNameList);
          axios.post(process.env.VUE_APP_API_URL + '/updateNameList', jsonUpdateNameList);
          var elt = document.getElementById('updatelist'+numlist);
          elt.classList.remove("showedupdatelist");
          elt.classList.add("hiddenupdatelist");
          var listname = document.getElementById('titlelist'+numlist);
          listname.innerHTML = inputtext;
        },
        updateNameTask: function(numtask) {
          var el = document.getElementById('inputupdatetask'+numtask);
          var inputtext = el.value;

          var updateNameTask = [{
                "idtask": numtask,
                "nametask": inputtext
          }];
          var jsonUpdateNameTask = JSON.stringify(updateNameTask);

          axios.post(process.env.VUE_APP_API_URL + '/updateNameTask', jsonUpdateNameTask);
          var elt = document.getElementById('updatetask'+numtask);
          elt.classList.remove("showedupdatetaskinput");
          elt.classList.add("hiddenupdatetaskinput");
          var taskname = document.getElementById('nametask'+numtask);
          taskname.innerHTML = inputtext;
        },
        updateStatusTask: function(numtask) {
          var el = document.getElementById('statustask'+numtask);
          var numstatustask;
          if (el.classList.contains('statustask0')) {
            numstatustask = 1;
          } else if (el.classList.contains('statustask1')) {
            numstatustask = 0;
          }
          var updateStatusTask = [{
                "idtask": numtask,
                "statustask": numstatustask
            }]; 
          var jsonUpdateStatusTask = JSON.stringify(updateStatusTask);
          axios.post(process.env.VUE_APP_API_URL + '/updateStatusTask', jsonUpdateStatusTask)
            .then(() => {
              if (el.classList.contains('statustask0')) {
                el.classList.remove('statustask0');
                el.classList.add('statustask1');
                el.innerHTML = 'Terminé';
              } else if (el.classList.contains('statustask1')) {
                el.classList.remove('statustask1');
                el.classList.add('statustask0');
                el.innerHTML = 'En cours';
              }
              var idlist;
              var progression;
              axios.get(process.env.VUE_APP_API_URL + '/updateProgressionList/' + numtask)
                .then(response => {
                  idlist = response.data['id_list'];
                  progression = response.data['progression'];
                  document.getElementById('progressionlist'+idlist).innerHTML = '('+progression+'%)&nbsp;';
                  });
            });
        },
        deleteList: function(idList) {
          axios.get(process.env.VUE_APP_API_URL + '/deleteList/' + idList)
            .then(() => {
                    axios.get(process.env.VUE_APP_API_URL + '/listsoftaskslists')
                      .then(response => (this.taskslists = response.data));
              }
            )          
        },
        deleteTask: function (idTask) {
          axios.get(process.env.VUE_APP_API_URL + '/deleteTask/' + idTask)
            .then(() => {
                  axios.get(process.env.VUE_APP_API_URL + '/listsoftaskslists')
                    .then(response => (this.taskslists = response.data));
            }
            )
        }
  },
  created() {
    axios.get(process.env.VUE_APP_API_URL + '/listsoftaskslists')
    .then(response => (this.taskslists = response.data));
  }
}

</script>
