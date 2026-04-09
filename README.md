# ajkjdksjd

// Service
// 6. Actualizar por id
    public Incidencia actualizar(Integer id, Incidencia incidenciaActualizar) {
        // Se asigna una id para que se actualize el registro que ya existe
        incidenciaActualizar.setId(id);

        return incidenciaRepository.save(incidenciaActualizar);
    }


// Controller
// 5. Metodo PUT: Actualizar una incidencia
    @PutMapping("/{id}")
    public ResponseEntity<?> actualizarIncidencia(@PathVariable Integer id, @Valid @RequestBody Incidencia incidencia) {
        try {
            // Se valida si existe una id para actualizar
            if (!incidenciaService.existePorId(id)) {
                // Si no existe, arroja NOT_FOUND
                return ResponseEntity.status(HttpStatus.NOT_FOUND)
                        .body("No existe una incidencia con ese id");

            }
            // Se actualiza la incidencia sin problema si se encuentra su id
            Incidencia incidenciaActualizar = incidenciaService.actualizar(id, incidencia);
            return ResponseEntity.status(HttpStatus.OK)
                    .body(incidenciaActualizar);
        } catch (Exception e) {
            return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR)
                    .body("No se ha actualizado una incidencia con ese id");
        }

    }
