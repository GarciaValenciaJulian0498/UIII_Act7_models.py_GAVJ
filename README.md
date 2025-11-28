# UIII_Act7_models.py_GAVJ
<img width="1274" height="692" alt="image" src="https://github.com/user-attachments/assets/8423d770-10af-49e3-86b2-0d2399313659" />

## Models.py
    from django.db import models
    
    class CategoriaSuper(models.Model):
        id_categoria = models.AutoField(primary_key=True)
        nombre_categoria = models.CharField(max_length=100)
        descripcion_categoria = models.TextField()
        pasillo = models.CharField(max_length=50)
        fecha_creacion = models.DateTimeField()
        es_perecedero = models.BooleanField()
    
        def __str__(self):
            return self.nombre_categoria
    
    
    class Proveedor(models.Model):
        id_proveedor = models.AutoField(primary_key=True)
        nombre_proveedor = models.CharField(max_length=100)
        contacto_persona = models.CharField(max_length=100)
        telefono = models.CharField(max_length=20)
        email = models.CharField(max_length=100)
        direccion_proveedor = models.CharField(max_length=255)
        ruc = models.CharField(max_length=20)
    
        def __str__(self):
            return self.nombre_proveedor
    
    
    class ProductoSuper(models.Model):
        id_producto = models.AutoField(primary_key=True)
        nombre_producto = models.CharField(max_length=255)
        descripcion = models.TextField()
        precio_unitario = models.DecimalField(max_digits=10, decimal_places=2)
        stock = models.IntegerField()
        categoria = models.ForeignKey(CategoriaSuper, on_delete=models.CASCADE)
        proveedor = models.ForeignKey(Proveedor, on_delete=models.CASCADE)
        fecha_vencimiento = models.DateField()
        codigo_barras = models.CharField(max_length=50)
        peso_gramos = models.IntegerField()
        tipo_empaque = models.CharField(max_length=50)
    
        def __str__(self):
            return self.nombre_producto
    
    
    class Cajero(models.Model):
        id_cajero = models.AutoField(primary_key=True)
        nombre = models.CharField(max_length=100)
        apellido = models.CharField(max_length=100)
        dni = models.CharField(max_length=20)
        fecha_contratacion = models.DateField()
        salario = models.DecimalField(max_digits=10, decimal_places=2)
        turno = models.CharField(max_length=50)
        telefono = models.CharField(max_length=20)
        email = models.CharField(max_length=100)
    
        def __str__(self):
            return f"{self.nombre} {self.apellido}"
    
    
    class ClienteSuper(models.Model):
        id_cliente = models.AutoField(primary_key=True)
        nombre = models.CharField(max_length=100)
        apellido = models.CharField(max_length=100)
        telefono = models.CharField(max_length=20)
        email = models.CharField(max_length=100)
        fecha_registro = models.DateField()
        puntos_fidelidad = models.IntegerField()
        direccion_cliente = models.CharField(max_length=255)
        fecha_nacimiento = models.DateField()
    
        def __str__(self):
            return f"{self.nombre} {self.apellido}"
    
    
    class VentaSuper(models.Model):
        id_venta = models.AutoField(primary_key=True)
        fecha_venta = models.DateTimeField()
        cajero = models.ForeignKey(Cajero, on_delete=models.CASCADE)
        cliente = models.ForeignKey(ClienteSuper, on_delete=models.CASCADE)
        total_venta = models.DecimalField(max_digits=10, decimal_places=2)
        metodo_pago = models.CharField(max_length=50)
        descuento_aplicado = models.DecimalField(max_digits=5, decimal_places=2)
        estado_venta = models.CharField(max_length=50)
        numero_ticket = models.CharField(max_length=50)
    
        def __str__(self):
            return f"Venta {self.id_venta}"
    
    
    class DetalleVentaSuper(models.Model):
        id_detalle = models.AutoField(primary_key=True)
        venta = models.ForeignKey(VentaSuper, on_delete=models.CASCADE)
        producto = models.ForeignKey(ProductoSuper, on_delete=models.CASCADE)
        cantidad = models.IntegerField()
        precio_unitario = models.DecimalField(max_digits=10, decimal_places=2)
        subtotal = models.DecimalField(max_digits=10, decimal_places=2)
        iva_aplicado = models.DecimalField(max_digits=5, decimal_places=2)
        descuento_item = models.DecimalField(max_digits=5, decimal_places=2)
    
        def __str__(self):
            return f"Detalle {self.id_detalle}"
