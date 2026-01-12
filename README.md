# exposici-n-
// La interfaz que queremos usar.
interface ILogger {
  log(message: string): void;
}

// La clase incompatible (ej. una librería externa).

class ExternalLogLibrary {
  public writeToConsole(text: string): void {
    console.log(`[External Lib]: ${text}`);
  }
}

//  Hace de puente entre el Target y el Adaptee.
class LoggerAdapter implements ILogger {
  private externalLib: ExternalLogLibrary;

  constructor(externalLib: ExternalLogLibrary) {
    this.externalLib = externalLib;
  }

  // Implementamos la interfaz que espera el cliente (log)
  // y delegamos la llamada al método incompatible (writeToConsole).
  public log(message: string): void {
    this.externalLib.writeToConsole(message);
  }
}

// --- EJECUCIÓN ---

// El cliente (tu código) no necesita saber cómo funciona la librería externa,
// solo interactúa con la interfaz ILogger.

const library = new ExternalLogLibrary();
const adapter: ILogger = new LoggerAdapter(library);

adapter.log("¡El patrón Adapter está funcionando!");
