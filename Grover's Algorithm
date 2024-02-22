namespace Quantum.GroverSearch {
    //we're defining our own namespace
    open Microsoft.Quantum.Measurement;
    //this namespace is useful for measurement functionalities

    // Here we're creating a quantum oracle

    //the parameters consist of a int array called mark item which consists of integers, (binary values) that represent the item that you're searching for within the quantum state.
    //And a qubits array that represent an array of qubits, which we're working with to mark the target item

    //the x gate flips the amplitudes between 1 and 0 to make it easier to identify


    operation Oracle(markItem : Int[], qubits : Qubit[]) : Unit is Adj { //
        for (idx in 0 .. Length(markItem) - 1) {
            if (markItem[idx] == 1) {
                X(qubits[idx]);
            }
        }
    }

    // Diffusion operator inverts the amplitudes 
    //the z gates  inverts the amplitudes between -1 and 1
    operation DiffusionOperation(markItem : Int[], qubits : Qubit[]) : Unit is Adj {
        let n = Length(markItem);
        let avg = Sum([Idx(item) * markItem[item] | item in 0 .. n - 1]) / IntAsDouble(n);
        //The Z gate sets up the quantum state by creating a state where marked items have a phase difference from unmarked items, 
        //facilitating the interference and amplification of the marked items during the algorithm's execution.
        for (qubit in qubits) {
            Z(qubit);
        }

        // In Grover's algorithm, applying the H gate to qubits corresponding to marked items helps amplify 
        // the probability amplitude of these items by putting them into superposition.
        for (idx in 0 .. n - 1) {
            if (markItem[idx] == 1) {
                H(qubits[idx]);
            }
        }
    }
    

    // Grover's algorithm
    // The markItem parameter represents the item(s) we are searching for in the database.
    // The n : int parameter represents the number of qubits used in the quantum register.
    operation GroverSearch(markItem : Int[], n : Int) : Result[] {
        mutable result = new Result[n];
        //here we initialize an array named result of size n to store the measurement results of the qubits.
        using (qubits = Qubit[n]) {
            H(qubits);
            
            // Number of iterations for amplitude amplification
            let numIterations = IntAsDouble(Sqrt(PowI(2, n)));
            
            repeat {
                Oracle(markItem, qubits);
                DiffusionOperation(markItem, qubits);
                set numIterations -= 1.0;
            } until (numIterations == 0.0);
            
            set result = ForEach(qubits, MeasureResult);
        }
        
        return result;
    }
}
