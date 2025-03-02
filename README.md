import React, { useState } from "react";

export default function GestionChicasMagicas() {
  const [magicalGirls, setMagicalGirls] = useState([
    {
      id: 1,
      name: "Madoka Kaname",
      age: 14,
      city: "Mitakihara",
      state: "rescatada",
      contractDate: "2023-01-01",
    },
    {
      id: 2,
      name: "Sayaka Miki",
      age: 14,
      city: "Mitakihara",
      state: "desaparecida",
      contractDate: "2023-02-10",
    },
    {
      id: 3,
      name: "Homura Akemi",
      age: 14,
      city: "Mitakihara",
      state: "activa",
      contractDate: "2023-03-15",
    },
  ]);

  const [filter, setFilter] = useState("all");
  const [newGirl, setNewGirl] = useState({
    name: "",
    age: "",
    city: "",
    state: "activa",
    contractDate: "",
  });

  const [editGirl, setEditGirl] = useState(null);

  const handleChange = (e) => {
    setNewGirl({ ...newGirl, [e.target.name]: e.target.value });
  };

  const addGirl = () => {
    if (
      !newGirl.name ||
      isNaN(newGirl.age) ||
      !newGirl.city ||
      !newGirl.contractDate
    ) {
      alert("Por favor, complete todos los campos correctamente.");
      return;
    }
    setMagicalGirls([
      ...magicalGirls,
      { ...newGirl, id: Date.now(), age: parseInt(newGirl.age) },
    ]);
    setNewGirl({
      name: "",
      age: "",
      city: "",
      state: "activa",
      contractDate: "",
    });
  };

  const deleteGirl = (id) => {
    setMagicalGirls(magicalGirls.filter((girl) => girl.id !== id));
  };

  const handleEditClick = (girl) => {
    setEditGirl(girl);
  };

  const handleEditChange = (e) => {
    setEditGirl({ ...editGirl, [e.target.name]: e.target.value });
  };

  const saveEdit = () => {
    if (
      !editGirl.name ||
      isNaN(editGirl.age) ||
      !editGirl.city ||
      !editGirl.contractDate
    ) {
      alert("Por favor, complete todos los campos correctamente.");
      return;
    }
    setMagicalGirls(
      magicalGirls.map((girl) => (girl.id === editGirl.id ? editGirl : girl))
    );
    setEditGirl(null);
  };

  return (
    <div
      className="p-5 font-sans text-white min-h-screen bg-cover bg-center flex flex-col items-center"
      style={{
        backgroundImage:
          "url('https://wallpapers.com/images/featured/madoka-magica-353masy1b7hjh7el.jpg')",
        backgroundSize: "cover",
        backgroundPosition: "center",
      }}
    >
      <h1 className="text-2xl font-bold bg-black bg-opacity-50 p-3 rounded">
        Gestión de Chicas Mágicas
      </h1>

      <label className="block mt-2 bg-black bg-opacity-50 p-2 rounded">
        Filtrar por estado:
        <select
          value={filter}
          onChange={(e) => setFilter(e.target.value)}
          className="ml-2 p-1 border rounded text-black"
        >
          <option value="all">Todas</option>
          <option value="activa">Activa</option>
          <option value="desaparecida">Desaparecida</option>
          <option value="rescatada">Rescatada</option>
        </select>
      </label>

      <h2 className="text-lg font-semibold mt-4 bg-black bg-opacity-50 p-2 rounded">
        Agregar Nueva Chica Mágica
      </h2>
      <div className="mt-2 p-4 border border-white rounded bg-black bg-opacity-50">
        <input
          type="text"
          name="name"
          placeholder="Nombre"
          value={newGirl.name}
          onChange={handleChange}
          className="p-1 m-1 border rounded text-black"
        />
        <input
          type="number"
          name="age"
          placeholder="Edad"
          value={newGirl.age}
          onChange={handleChange}
          className="p-1 m-1 border rounded text-black"
        />
        <input
          type="text"
          name="city"
          placeholder="Ciudad"
          value={newGirl.city}
          onChange={handleChange}
          className="p-1 m-1 border rounded text-black"
        />
        <select
          name="state"
          value={newGirl.state}
          onChange={handleChange}
          className="p-1 m-1 border rounded text-black"
        >
          <option value="activa">Activa</option>
          <option value="desaparecida">Desaparecida</option>
          <option value="rescatada">Rescatada</option>
        </select>
        <input
          type="date"
          name="contractDate"
          value={newGirl.contractDate}
          onChange={handleChange}
          className="p-1 m-1 border rounded text-black"
        />
        <button
          onClick={addGirl}
          className="p-2 m-2 bg-green-500 text-white rounded"
        >
          Agregar
        </button>
      </div>

      <div className="mt-4 w-full flex flex-col items-center">
        {magicalGirls
          .filter((girl) => filter === "all" || girl.state === filter)
          .map((girl) => (
            <div
              key={girl.id}
              className="border p-4 mt-2 bg-black bg-opacity-50 border-white rounded w-80"
            >
              {editGirl && editGirl.id === girl.id ? (
                <>
                  <input
                    type="text"
                    name="name"
                    value={editGirl.name}
                    onChange={handleEditChange}
                    className="p-1 m-1 border rounded text-black"
                  />
                  <input
                    type="number"
                    name="age"
                    value={editGirl.age}
                    onChange={handleEditChange}
                    className="p-1 m-1 border rounded text-black"
                  />
                  <input
                    type="text"
                    name="city"
                    value={editGirl.city}
                    onChange={handleEditChange}
                    className="p-1 m-1 border rounded text-black"
                  />
                  <select
                    name="state"
                    value={editGirl.state}
                    onChange={handleEditChange}
                    className="p-1 m-1 border rounded text-black"
                  >
                    <option value="activa">Activa</option>
                    <option value="desaparecida">Desaparecida</option>
                    <option value="rescatada">Rescatada</option>
                  </select>
                  <input
                    type="date"
                    name="contractDate"
                    value={editGirl.contractDate}
                    onChange={handleEditChange}
                    className="p-1 m-1 border rounded text-black"
                  />
                  <button
                    onClick={saveEdit}
                    className="p-2 mt-2 bg-blue-500 text-white rounded"
                  >
                    Guardar
                  </button>
                </>
              ) : (
                <>
                  <h2 className="font-semibold">{girl.name}</h2>
                  <p>
                    <strong>Edad:</strong> {girl.age}
                  </p>
                  <p>
                    <strong>Ciudad:</strong> {girl.city}
                  </p>
                  <p>
                    <strong>Estado:</strong> {girl.state}
                  </p>
                  <p>
                    <strong>Fecha de contrato:</strong> {girl.contractDate}
                  </p>
                  <button
                    onClick={() => handleEditClick(girl)}
                    className="p-2 mt-2 bg-yellow-500 text-white rounded"
                  >
                    Editar
                  </button>
                  <button
                    onClick={() => deleteGirl(girl.id)}
                    className="p-2 mt-2 bg-red-500 text-white rounded"
                  >
                    Eliminar
                  </button>
                </>
              )}
            </div>
          ))}
      </div>
    </div>
  );
}

