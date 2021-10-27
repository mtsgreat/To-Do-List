<template>
  <!-- LEMBRETE: CRIAR MODO FOCO, BOTÃO PARA TIRAR O FORM DE INSERIR E DEIXAR AS TASK FULL PAGE -->
  <div class="form-list" v-show="focus">
    <h1>Adicionar Lembrete<i class="fas fa-thumbtack"></i></h1>

    <div class="input-form">
      <input
        class="input-text"
        type="text"
        v-model="item.nome"
        placeholder="Adicine uma tarefa na lista.."
      />
    </div>
    <div class="input-form">
      <input
        class="btn"
        type="submit"
        value="Adicionar"
        @click.prevent="addItem"
      />
    </div>
  </div>
  <div class="focus-mode">
    <span @click.prevent="focusModeActive"><i class="fas fa-expand"></i></span>
  </div>
  <div class="painel" id="focus">
    <div class="card">
      <ul class="lista">
        <li v-for="(item, itemsChave) in items" :key="itemsChave">
          {{ item.nome }}
          <input
            type="submit"
            value="Excluir"
            @click.prevent="deleteItem(item.id)"
          />
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "FormTask",
  data() {
    return {
      focus: true,
      items: [],
      item: {
        id: "",
        nome: "",
      },
    };
  },
  methods: {
    focusModeActive() {
      if (this.focus == true) {
        document.getElementById("focus").style.width = "100%";
        this.focus = false;
      } else {
        document.getElementById("focus").style.width = "65%";
        this.focus = true;
      }
    },
    addItem() {
      if (this.item.nome == "") {
        alert("Preencha o campo!!");
      } else {
        let items = localStorage.getItem("itemsChave");

        //gerador de ID
        this.item.id = new Date().getTime();

        if (items) {
          items = JSON.parse(items);
          items.push(this.item);
        } else {
          items = [this.item];
        }

        //fazer atualização do array
        this.items = items;

        localStorage.setItem("itemsChave", JSON.stringify(this.items));

        window.location.reload();
      }
    },
    deleteItem(id) {
      let items = localStorage.getItem("itemsChave");

      if (!items) return;

      items = JSON.parse(items);

      items = items.filter((item) => {
        return item.id != id;
      });

      /* fazendo atualização no array */
      this.items = items;

      localStorage.setItem("itemsChave", JSON.stringify(items));
    },
  },
  created() {
    this.items = JSON.parse(localStorage.getItem("itemsChave"));
  },
};
</script>

<style scoped>
.form-list {
  width: 35%;
  height: 100vh;
  background-color: black;
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  border-radius: 0 20px 20px 0;
  border-right: solid #ccc 6px;
  box-shadow: 0 0 10px 5px #ccc;
}

.form-list h1,
.input-form {
  margin-bottom: 5%;
}

h1 {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 40px;
  color: white;
}

i.fas.fa-thumbtack {
  margin-left: 2%;
  transform: rotate(35deg);
}

.input-text {
  height: 20px;
  width: 400px;
  padding: 2%;
  border: none;
  outline: none;
  border-radius: 5px;
  font-size: 20px;
  transition: 0.5s;
}

.input-text:focus-within {
  box-shadow: 0 0 10px 5px #ccc;
  transition: 0.5s;
}

.btn {
  height: 40px;
  width: 35%;
  border: none;
  font-size: 17px;
  border-radius: 5px;
  color: black;
  background-color: white;
  cursor: pointer;
}

.btn:hover {
  box-shadow: 0 0 10px 5px #ccc;
}

.painel {
  /*  border: solid; */
  width: 65%;
  display: flex;
  justify-content: center;
  align-items: center;
}

ul.lista {
  padding: 10px;
}

ul.lista li {
  list-style: auto;
  margin: 15px;
  font-size: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.card .lista li input {
  border: none;
  padding: 10px;
  margin-left: 20px;
  background-color: red;
  color: white;
  border-radius: 8px;
  font-weight: 900;
  cursor: pointer;
}

.card .lista li input:hover {
  background-color: rgba(255, 0, 0, 0.479);
  transition: 0.5s;
}

.focus-mode {
  position: absolute;
  width: 215px;
  top: 25px;
  left: 10px;
}

i.fas.fa-expand {
  color: red;
  font-size: 50px;
  cursor: pointer;
  transition: 0.5s;
  border: solid white 3px;
  padding: 3px;
  border-radius: 5px;
  box-shadow: 0 0 10px 5px #ccc;
}

i.fas.fa-expand:hover {
  font-size: 60px;
  transition: 0.5s;
}
</style>
